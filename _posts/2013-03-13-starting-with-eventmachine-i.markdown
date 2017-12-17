---
title: Starting with EventMachine I
lang: en
picture: https://s3.amazonaws.com/javieracero.com/event-machine1.jpg
excerpt: Earlier this year I wrote a couple ruby programs using EventMachine. I found it hard to start with it and the documentation or tutorials scarce. Let's fix that.
layout: post
---

This blog post is an extract of an ebook about EventMachine that I started
writing some time ago. Somehow it ended up half written in some dark corner
of my hard drive. I have decided to publish the material I have as series of
posts. **Please let me know if you find the material useful.**

You can all the posts here:

- [Starting with EventMachine I](/blog/starting-with-eventmachine-i)
- [Starting with EventMachine II](/blog/starting-with-eventmachine-ii)
- [Starting with EventMachine III](/blog/starting-with-eventmachine-iii)
- [Starting with EventMachine IV](/blog/starting-with-eventmachine-iv)

## What's EventMachine
What's EventMachine you may be wondering? EventMachine is an event-driven I/O and lightweight concurrency library for Ruby. It provides an API to handle many different protocols and the ones that are not distributed with it can be found as gems.

### Hello evented world
Many blog posts and talks about EventMachine use an [echo server and client](http://en.wikipedia.org/wiki/Echo_Protocol) to show how the library works. Is kind of the *hello world* version of libraries that deal with concurrency. Even though it's a great example of how easy it is to create servers and connect to them with EventMachine I don't think it's a good way of getting started.

We are going to start simple. Our first program will be the closest it can get to the usual *hello world* but with an evented flavour. We will:

1. Start EventMachine.
2. Create a time based event that will trigger after 2 seconds.
3. Create a callback that handles that event which will print the message *"Hello world"* and stop EventMachine.

The first thing you need to do to get started is installing EventMachine. This one will be easy. It's distributed as a gem so you can install it by running:

    gem install eventmachine

You will need to require it in order to use it in your program:

<pre><code data-language="ruby">require 'eventmachine'</code></pre>

Once you have done that you are set to write your first EventMachine powered application: an event powered *hello world!* (the time formatting has been omitted for simplicity):

<pre><code data-language="ruby">EventMachine.run do
  puts "starting EventMachine at \#{format_as_hhmmss(Time.now)}"
  EM.add_timer(2) do
    puts "Hello world"
    puts "stopping EventMachine at \#{format_as_hhmmss(Time.now)}"
    EM.stop
  end
end</code></pre>

You may have noticed that I have used both `EventMachine` and `EM`. In the library codebase you can find this line:

<pre><code data-language="ruby">EM = EventMachine</code></pre>

Both modules are the same thing. `EM` is just an alias created for convenience so we don't need to type the whole name every single time.

When you run this code the first thing you will see will be the time EventMachine was started at. Two seconds later the *Hello world* will be printed out and, almost simultaneously, the stopping message:

    starting EventMachine at 10:35:56
    Hello world
    stopping EventMachine at 10:35:58

### What does `EM.run` do?
The method `run` starts EventMachine's event loop. Don't worry if you have no idea of what an *event loop* is: you you will by the end of this chapter. Once started it traps the thread it runs in, so the code won't continue running until it's stopped. For now you can think of it being a `while(true)` loop.

`EM.run` takes a block. The block will be yielded **right before** the event loop is booted. That means this is the place to setup everything your application may need.

### What does `EM.stop` do?
As you may have figured out, the `stop` method halts the event loop and returns the control to the thread that started it.

Calling this method will stop EventMachine almost immediately (we will learn what *almost immediately* means when we dig deeper into how the event loop works). It will wait for no event to be triggered and no callback to be run. That means we need to be careful with when and how we stop EventMachine.

### What does `EM.add_timer` do?
By calling this method you are setting up your first event handler or callback. You are telling EventMachine to watch for an event: *two seconds passing by*. Once that event is triggered (once two seconds pass by), EventMachine will run the block you passed to `EM.add_timer`.

Here is where you can see the [*Hollywood Principle*](http://en.wikipedia.org/wiki/Hollywood_principle) applied. Usually you call other application's code. Whether they are gems, frameworks or APIs it is your code who calls them. In this case it will be the other way around: the library will be the one calling the code you wrote. It's a very common pattern to deal with asynchrony.
