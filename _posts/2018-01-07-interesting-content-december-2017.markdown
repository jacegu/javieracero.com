---
title: Interesting content (December 2017)
lang: en
picture: https://s3.amazonaws.com/javieracero.com/interesting-content-december-2017.jpg
excerpt: Interesting books, talks and blog posts I have viewed or read during December 2017 and that I consider worth sharing for one reason or another.
layout: post
---

Happy New Year everyone! I'm starting 2018 trying to go back to writing here from time to time.

## Talks

### The “right” way to ship software

By [Jocelyn Goldfein](https://www.linkedin.com/in/jgoldfein/) former Engineer Director at Facebook (2010-2014) and  VP of Engineering at VMWARE (2003-2010). The talk took place as part of [hack.summit() 2016](https://hacksummit.org/).

I [found this one](http://www.eferro.net/2017/12/it-depends-jocelyn-goldfin-model-for.html) thanks to [@eferro](https://twitter.com/eferro).

It's a really thoughtful talk on how the way software is released is totally dependent on the context, and how it shapes companies, practices and the way we build software in general. **Must watch**. One of those talks that put into words things that seem obvious, but aren't.

[**Watch it here**](https://www.youtube.com/watch?v=VmYvJ3kDIWE).


### Evolutionary architectures

Saw a few talks on the same topic:

- One by Rebecca Parsons ([@rebeccaparsons](https://twitter.com/rebeccaparsons)) CTO at ThoughtWorks. [**Watch it here**](https://www.youtube.com/watch?v=OU_NKGEVsy8).
- One by Neal Ford ([@neal4d](https://twitter.com/neal4d)) from ThoughtWorks.  [**Watch it here**](https://www.youtube.com/watch?v=CglSFhwbI3s).
- One by Pat Kua ([@patkua](https://twitter.com/patkua)) CTO at N26, former ThoughtWorks.  [**Watch it here**](https://www.youtube.com/watch?v=7e6Ww8b2hzQ).

I got these from [this Twitter thread](https://twitter.com/GermanDZ/status/939258688048648193).

Talks present a, somewhat different, view of software architecture explaining how it can, and should, be the vehicle to allow guided, incremental, change.

Love the underlying concept and will certainly investigate more about the topic (in fact [the book they wrote](http://shop.oreilly.com/product/0636920080237) is already in my iPad and I'm looking forward to start it).

Neal's and Pat's are really the same talk delivered by two separate speakers. I liked Neal's better. Rebecca's is slightly different and addresses other interesting ideas. I re-watched Rebecca's after watching Neal's (and Pat's) and I think you'll get more value if you watch them in that order. Don't expect technical details as the talks (and the topic) are more high level.


## Books

### Clean Architecture (Uncle Bob)

It's been almost 6 years since [_Architecture: The Lost Years_](https://www.youtube.com/watch?v=WpkDN78P884) was published. That talk shook my world and caused quite some noise in the Ruby community. It pointed out everything that is wrong with _The Rails Way_ (aka _The Framework Way_). The main complian about the talk was that it didn't include any examples.

> The database is a detail.
> The web is a detail.
> Frameworks are not your application.

Unfortunately the book doesn't go much further than all the previous content that the author had already shared in blog posts, [Clean Coders](https://cleancoders.com/) videos or talks. In that sense, it's a _"greatest hits compilation"_. Most people will expect an in-depth example and won't find it in the book either.

There are two things that I really enjoyed though:

- **Part II**

  In this section the author discusses the 3 main programming paradigms (Procedural, Object Oriented and Functional). It goes over the main traits of each one and explains how each one of them imposes restrictions on the programmer, which is a point of view that I had never heard of before.

- **The epilogue.**

  I'd buy the book only to read it.

  In it the author goes over most of his career explaining what companies did he work for and what he did there. He explains the challenges he faced and what they did about them at the time. All of it sauced with pictures of the old computers and different devices that they were using at the time.


### The Nature of Software Development (Ron Jeffries)

I was expecting a more technical book. I had read good reviews by some peers and went for it without really knowing what the book was about. Got very little out of it because I was familiar with most of the ideas discussed in it.

> “Don't worry—we’re not going to drop into programming—but we do want all our readers to be aware of what the business needs to expect of developers, and what it needs to support.”

It's short and easy to read. Goes to the point and justifies everything clearly. It even points out something that most books about software processes ignore: to be able to build software iteratively (aka Agile Software Development) you need skilled developers.

Even though I didn't get much out of it, I must say that, if I have ever have to recommend one book to anyone as an introduction to iterative software development, it will be this one. It is _that_ good.


## Posts

### Managing your personal tech portfolio

This post got to my twitter feed (was retweeted by Neal Ford). Went through it quickly as it’s an easy read. It contains good advice to structure your learning. Most tips you probably have heard before, but I found two ideas really interesting:
1. Treating it as an investment portfolio was really appealing to me.
2. Having your own [technology radar a la ThoughtWorks](https://www.thoughtworks.com/radar) to guide learning.

[**Read it here**](https://crswlls.wordpress.com/2017/12/11/managing-your-personal-tech-portfolio/)


### Excuses by Uncle bob.

I follow Uncle Bob, but it ended up in my timeline retweeted by several people I follow.

What can I say, I love pro-TDD rants and this post is one of those. I have tried to stay away from rants against or in favor of TDD for the last 4 years. I can't believe our industry is still debating about this...

[**Read it here**](http://blog.cleancoder.com/uncle-bob/2017/12/18/Excuses.html)


### Elixir code quality tools by Matt Gauger

This one was part of [Elixir Radar](http://plataformatec.com.br/elixir-radar/) issue 123.

Although I’m not a big fan of these type of tools (specially Rubocop), there are some useful ones in this post.

[**Read it here**](http://blog.mattgauger.com/2017/11/21/elixir-code-quality-tools)
