---
title: Interesting content (January 2018)
lang: en
picture: https://s3.amazonaws.com/javieracero.com/interesting-content-january-2018.jpg
excerpt: Interesting books, talks and blog posts I have viewed or read during January 2018 and that I consider worth sharing for one reason or another.
layout: post
---

Running a little late this month, but here we go:

## Talks

### The art of destroying software by Greg Young

This one comes, again, from [@eferro](https://twitter.com/eferro) and his post about [_Simplicity for developers_](http://www.eferro.net/2017/10/simplicidad-para-desarrolladores.html). I've been watching most of those talks in the past few weeks.

I loved this talk, even if it’s a guy talking to the camera for 40 minutes without slides. I usually enjoy all Greg Young's talks. This one wasn't an exception.

The main idea behind it is to focus on building systems from pieces (objects, actors, micro-services, components...) that you can easily delete and re-write. This has a lot of implications, specially when talking about technical debt.

The other main takeaway from the talk is that we are doing nothing new. This is something that you will hear from other reputed professionals: Uncle Bob shares this very same idea in Clean Architecture several times. [Gary Bernhart](https://destroyallsoftware.com) has said the same thing in numerous occasions.


## Books

January was a busy month, including a DNSimple meetup in Florida. I continued reading [99 bottles of OOP](https://www.sandimetz.com/99bottles/). I have just finished reading it but the review will have to wait until next month.

In the meantime you can [watch this hypnotic video](https://www.instagram.com/p/Bd-tZ4-HNvQ/) that [@sbastn](https://twitter.com/sbastn) and I recorded on a windy day at Melbourne Beach.


## Posts

### Auto-squashing git commits by Thought Bot

This one [came into my twitter timeline thanks to @amuino](https://twitter.com/amuino/status/943130121975881729) back in December but I didn't have the chance to read it until January...

It introduces a couple features that you can use when rebasing that I wasn't familiar with. It may encourage me to rebase more often than I usually do.

[**Read it here**](https://robots.thoughtbot.com/autosquashing-git-commits)


### Stop abusing NotImplementedError

I found this post in the comments of [a talk on Youtube](https://www.youtube.com/watch?v=rK8yHl0cHoc). Funny enough the author seems to have deleted it.

It explains why we should not use `NotImplementedError` when trying to mimic interfaces or abstract classes in Ruby. This is, to my knowledge, a widely used practice. Finding out about the details of this error was very enlightening to me.

[**Read it here**](http://chrisstump.online/2016/03/23/stop-abusing-notimplementederror/)


### The modern dev team

This one was dropped in the [DNSimple](https://dnsimple.com) Slack channel.

There are 2 things that made me enjoy this post a lot:

1. Reflects on the fact that we keep resolving the same problems with different tools. Also says that Erlang solved this problems a long time ago and got most of the solutions right (which is a thought that I keep having more and more often).
2. Shares the view of a developer that just turned 50. We will all get there (🤞), so reading about the fears that will come may make it easier to grow older as a software engineer.

[**Read it here**](https://rob.conery.io/2018/01/22/the-modern-dev-team/)


### Don’t cross the beams by Kent Beck

This is one was referenced on [99 bottles of OOP](https://www.sandimetz.com/99bottles/). Like pretty much everything that Kent Beck writes, this is a must read.

The post explains the difference between vertical and horizontal refactorings and why you should perform them in order rather than mix them.

[**Read it here**](https://www.facebook.com/notes/kent-beck/dont-cross-the-beams-avoiding-interference-between-horizontal-and-vertical-refac/260531380646400/)
