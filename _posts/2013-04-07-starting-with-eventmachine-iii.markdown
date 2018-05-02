---
title: Starting with EventMachine III
lang: en
picture: https://s3.amazonaws.com/javieracero.com/event-machine3.jpg
excerpt: The event loop and reactor pattern are the two patterns EventMachine is powered by . Understanding them is key to write successful EventMachine applications.
layout: post
---

This blog post is an extract of an ebook about EventMachine that I started
writing some time ago. Somehow it ended up half written in some dark corner
of my hard drive. I have decided to publish the material I have as series of
posts. **Please let me know if you find the material useful.**

You can find all posts here:

- [Starting with EventMachine I](/blog/starting-with-eventmachine-i)
- [Starting with EventMachine II](/blog/starting-with-eventmachine-ii)
- [Starting with EventMachine III](/blog/starting-with-eventmachine-iii)
- [Starting with EventMachine IV](/blog/starting-with-eventmachine-iv)

## Just enough about patterns

In the [*hello world* example](/blog/starting-with-eventmachine-i) we talked about something called the *event loop*. The *event loop* is one of the two patterns EventMachine is powered by. Although you could use the library without really knowing anything about this patterns, understanding how they work will make a huge difference. There are certain features and bad practices that wouldn't make sense otherwise.

We are going to overview both patterns but it's going to be a really brief introduction. Later in the book we will develop our own reactor and event loop to get a better grasp of their internals.

### The reactor
The reactor is an event handling pattern designed to manage service requests that are delivered concurrently to an application. It was conceived with the [C10K problem](http://www.kegel.com/c10k.html) in mind.

The reactor has to be aware of the different service requests or events it will be watching for and their corresponding handlers or callbacks. Those events will come through a set of resources or *handles*. In EventMachine the *handles* will be I/O resources like sockets or file descriptors.

Once initialized, the reactor will enter a phase known as *event demultiplexing phase*. During this stage it will poll the resources for a very sort time span waiting for events to happen. Once an event is triggered in one of the *handles*, the registered callback for that event, in that particular resource, will be dispatched.

With this newly acquired knowledge we can rephrase what the `EM.run` method does: it boots EventMachine's reactor taking a block that will be yielded right before it enters the *event demultiplexing phase*. That is, prior to starting the event loop.

### The event loop
The *event loop* is EventMachine's reactor's event demultiplexer.

When the reactor enters this phase it gets trapped in a loop[^C1_06]. Each of the iterations through this loop is known as a *reactor tick* or just *tick*. During each of them the reactor performs the same three actions:

- Check whether enough time has passed by for a timer event to be triggered. It will handle those events by calling the set up callbacks.
- Check if any of the handled resources is ready to be read or written and trigger the corresponding event. EventMachine uses the [select](http://en.wikipedia.org/wiki/Asynchronous_I/O#Select.28.2Fpoll.29_loops)[^C1_05] system call to poll the *handles* which is widely available on UNIX and Windows platforms.
- Check for dead connections. If an inactivity timeout was set and enough time has passed by without getting any information, the connection will be closed.

Prior to each these three actions EventMachine's reactor checks whether the `stop` method has been called. If it wasn't called the event loop continues otherwise the loop is broken[^C1_07] and the reactor exits the event demultiplexing phase.


[^C1_05]: Latest versions of EventMachine can also use a better mechanism where available called `epoll`
[^C1_06]: Quite literally because it uses Ruby's `loop` construct
[^C1_07]: Again, literally calling `break`

Putting all this together the loop's pseudocode would look like this:

<pre><code data-language="ruby">loop do
  break if stop_was_called?
  trigger_time_based_events

  break if stop_was_called?
  select_handles

  break if stop_was_called?
  close_dead_connections
end</code></pre>


### Revisiting the *hello world* example
That's all you need to know about the reactor and the event loop right now. Obviously there are a lot of subtleties on how EventMachine works but the basics are covered. This brief explanation will make a huge difference when you try to understand how the library primitives work out.

In fact, it will already pay of. With our current level of understanding of how EventMachine works we can explain the behaviour of the second version of our *hello world* application. Let me refresh your memory:

<pre><code data-language="ruby">EM.run do
  puts "starting EventMachine at \#{format_as_hhmmss(Time.now)}"
  EM.add_timer(0) { puts "Hello world" }
  EM.stop
  puts "stopping EventMachine at \#{format_as_hhmmss(Time.now)}"
end</code></pre>

We got both messages as output even though we were calling `EM.stop` before printing the second message. We also didn't get the *hello world* message despite it should be printed in response to 0 seconds passing by:

    starting EventMachine at 17:17:37
    stopping EventMachine at 17:17:37

Lets think carefully on what's going on. All the code we have is inside the block we are passing to `EM.run`. That means it will be executed before the reactor enters the *event demultiplexing phase*. Before the event loop is started both messages will be printed, an event handler for the event *0 seconds passing by* is set up and `EM.stop` is called.

When the loop starts, the first thing the reactor will do is checking if `stop` has been called, even before checking if there are timer events to be triggered. It will find that the stop has been scheduled and break the loop immediately. The reactor will check the timers not even once.
