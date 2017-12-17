---
title: The smell of that potion
lang: en
picture: https://s3.amazonaws.com/javieracero.com/the-smell-of-that-potion.jpg
excerpt: Some thoughts on Ruby, Rails, Elixir and Phoenix and how libraries, frameworks and communities influence the practices and the sustainability of languages.
layout: post
---

I've been using [Ruby](https://www.ruby-lang.org) as my main programming language since 2010. As of today I still enjoy its syntax and simplicity. Its community is very friendly and productive and many companies and products have sprung from it.

However all these years have not been a path of roses. I have seen how the Ruby community has been deeply influenced by one big project: [Ruby on Rails](http://rubyonrails.org/). The standards and conventions of that project were taken as the right way of using the language. There have been [plenty](http://blog.steveklabnik.com/posts/2011-12-30-active-record-considered-harmful) of [voices](http://confreaks.tv/videos/goruco2012-hexagonal-rails) [complaining](http://solnic.eu/2015/06/06/cutting-corners-or-why-rails-may-kill-ruby.html) about it yet the mainstream mentality hasn't changed one bit.

The other problem that any Ruby developer will face sooner rather than later is performance. If there were people in the community warning about the Rails way of doing things the complains about the performance have been an outcry.

It's been three years since this thought crossed my mind for the first time and I still think that **Rails and the [GIL](https://en.wikipedia.org/wiki/Global_interpreter_lock) will kill[^C1_1] Ruby**. There are countless examples of how bad the maintainability of Rails applications gets as the code base grows. You will find even more cases of performance issues. There is a lesson to be learnt lurking in there. A lesson that I won't easily forget when I choose my next go-to programming language.

[^C1_1]: And by killing I mean significantly impacting the usage of the language.


Speaking of which: I have been playing with [Elixir](http://elixir-lang.org) lately. It was a young language back in 2013 when I first tried it out. It's more mature now. Several libraries and [frameworks](http://www.catonmat.net/blog/frameworks-dont-make-sense/) are making the language ecosystem more interesting. One of these projects is [Phoenix](http://www.phoenixframework.org/).

Phoenix is a mayor player in the language now. Big enough to make creating a new Phoenix project a task in the language build tool, `mix`.

I have to admit that I haven't given the framework a serious try yet. But all the demos and guides I have seen reminded me so much of Rails that I wanted to `brew uninstall elixir` immediately. While performance won't be an issue, maintainability and bad practices may turn Elixir into the new Ruby.

It was a relief to find [this article](http://blog.plataformatec.com.br/2015/10/mocks-and-explicit-contracts/) by José Valim (the creator of Elixir) while researching about testing and mocking tools. That blog post is a summary of the mocking and testing practices that I have been following and advocating for several years. I was super pleased not only to see that José advocates them too but also that the language has support for them right out of the box.

I am looking forward to give Phoenix a try. Hope all that Rails-iness is only a coat intended to create familiarity. Hope Elixir and its community embraces modularity and good design practices like Ruby never did. My fingers are crossed.
