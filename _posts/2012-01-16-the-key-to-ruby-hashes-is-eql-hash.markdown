---
title: "The key to Ruby hashes is eql? hash"
lang: en
excerpt: I've been struggling for a few hours with key hashes in Ruby. We usually use primitive values as keys but what happens when we want to use one of our objects.
layout: post
---

Yesterday I spent a couple hours trying to resolve this little Ruby riddle:

<pre><code data-language="ruby">class Key
  attr_reader :value

  def initialize(value)
    @value = value
  end
end

k1 = Key.new('foo')
k2 = Key.new('foo')

h = { k1 => 'bar' }
puts h.has_key? k1 # -> true
puts h.has_key? k2 # -> false ??</code></pre>

I have been programming in Ruby for more than a year now. I have used the `Hash` class a myriad of times. But the thing is I've only used it with primitive values as keys.  Usually a `String` or `Symbol`.

Yesterday I tried to use an instance of a class I just defined as a key of the hash.  The first time, when calling the `has_key?` method I wasn't surprised. My Java past surfaced and `equals` pop into my mind. So I made the class `Comparable`.

<pre><code data-language="ruby">class Key
  include Comparable

  attr_reader :value

  def initialize(value)
    @value = value
  end

  def &lt;=&gt;(other_key)
    value &lt;=&gt; other_key.value
  end
end

k1 = Key.new('foo')
k2 = Key.new('foo')

h = { k1 => 'bar' }
puts h.has_key? k1 # -> true
puts h.has_key? k2 # -> still false ??:·(
</code></pre>

As you may expect, the result was the same and I was starting to get really frustrated. I implemented any other method of equality I counld think about. No results. I started hitting walls with my forehead and blaming the flue I currently have. I thought I was missing something obvious.

Once the wall started to crack I remembered having read something about hash keys in the Pragmatic Programmers' [Programming Ruby 1.9](http://pragprog.com/book/ruby3/programming-ruby-1-9) book. I went straight away to look it up and here is what I found:

<blockquote>Hash keys must respond to the message `hash` by returning a hash code, and the hash code for a given key must not change. The keys used in hashes must also be comparable using `eql?`. If `eql?` returns `true` for two keys, then those keys must also have the same hash code. This means that certain classes (such as `Array` and `Hash`) can’t conveniently be used as keys, because their hash values can change based on their contents.
<cite>Programming Ruby 1.9, Pragmatic Programmers</cite></blockquote>

So the `hash` and `eql?`  methods were the little mystery and the key to solving the problem. (In Java, you also have the `hashCode` method besides `equals`, but I didn't remember it because Eclipse always generated it for me...)

All primitive types we normally use as hash keys `Integer`, `String` and `Symbol` have a proper implementation of these methods. When you don't define them they default to the ones in `Object` which are based on object identity. That's why `h.has_key? k1` returns `true`.

<pre><code data-language="ruby">class Key
  attr_reader :value

  def initialize(value)
    @value = value
  end

  def eql?(other_key)
    value == other_key.value
  end

  def hash
    value.hash
  end
end

k1 = Key.new('foo')
k2 = Key.new('foo')

h = { k1 => 'bar' }
puts h.has_key? k1 # -> true
puts h.has_key? k2 # -> true</code></pre>

I added the methods and the quiz was solved but I'm still embarrassed and still feel like a Ruby beginner.
