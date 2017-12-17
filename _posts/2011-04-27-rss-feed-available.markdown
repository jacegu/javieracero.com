---
title: RSS feed available
lang: en
excerpt: "The RSS feed is now available. Check out what I researched about the RSS specfication and how I have developed the feed using HAML and Sinatra."
layout: post
---

As you might have noticed the RSS feed has been available since a few hours ago. You can access to it from the URL [http://javieracero.com/blog/rss](http://javieracero.com/blog/rss) and soon enough there will be a link on the sidebar.

I was expecting many of you to ask for RSS feed feature soon. That's why It was the next backlog story I was going to work on. The plan was to have it ready by the end of the week but I have rushed things up. Thanks to [HAML](http://haml-lang.com) it was ready in a few minutes.

## Developing the RSS feed

### Specification

I had never developed an RSS feed before so **most of the work was learning about the specification**. It turns out that there are a few alternatives regarding feeds. You have to choose between Atom and a few versions of RSS: 0.91, 0.92, 1.0 and  2.0 (or just put them all). It may be trickier than you think since there are incompatibility issues between versions.


I have followed the [RSS 2.0 specfication](http://cyber.law.harvard.edu/rss/rss.html). In the future I might add an Atom feed just to learn about the differences between it and RSS.

### Generating the XML

**An RSS feed is just a plain XML file**. Given that the blog engine makes an extensive use of HAML I had the prefect tool for the job.

I decided to treat the XML file as a regular view althougt I could have generated it from code. Just feels easier to maintain this way. It's like the about page, with the difference of generating XML instead of HTML.

Once the view was created I **added the route mapping** to my `Sinatra::Application` class which I have called `MyBlog::Engine` and provide the required data to the view before rendering it.


In this case I just had to pull the `@posts = @repository.published` statement to a `before` filter mapped to the route `/blog*` and job done.

### The result

The HAML file is just what you see in this Gist:

<pre><code data-language="html">!!! XML
%rss(version="2.0"
    xmlns:content="http://purl.org/rss/1.0/modules/content/"
    xmlns:atom="http://www.w3.org/2005/Atom")

%channel
  %title Javier Acero's blog
  %link #{url('blog/rss')}
  %atom:link(href="#{url('blog/rss')}"
             rel="self"
             type="application/rss+xml")
  %description
    This is where Javier Acero records what he learns
    about software development and where he reflects
    about his long road.
  %language en-US
  %lastBuildDate \#{@posts[0].utc_publication_time.to_rfc822}
  %webMaster j4cegu@gmail.com (Javier Acero)
  %managingEditor j4cegu@gmail.com (Javier Acero)

  -@posts.each do |post|
    %item
      %title \#{post.title}
      %link  \#{url('blog/'+ post.url)}
      %description \#{post.description}
      %author j4cegu@gmail.com (Javier Acero)
      %pubDate \#{post.utc_publication_time.to_rfc822}
      %guid(isPermaLink='true') \#{url('blog/'+ post.url)}
      %comments \#{url('blog/' + post.url + '#disqus_thread')}
      %content:encoded <![CDATA[\#{post.render_body}]]> </code></pre>

Of course there is room for improvement. But it's just good enough right now.

### Validation

Finally I validated the feed using the [ W3C feed validation service](http://validator.w3.org/feed/). I had to fix a typo and adequate the dates to the RFC822 format.

Piece of cake :·)
