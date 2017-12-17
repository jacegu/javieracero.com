---
title: A useful shell function
lang: en
picture: https://s3.amazonaws.com/javieracero.com/useful-function.jpg
excerpt: Nowadays it's very common to put some of your configuration values, like API secrets, in environment variables. But dealing with those variables can be painful.
layout: post
---

In last week's
[Ruby Weekly](http://rubyweekly.com)
one of the
[recommended posts](http://daniel.fone.net.nz/blog/2013/05/20/a-better-way-to-manage-the-rails-secret-token/)
was about a gem called
[Dotenv](https://github.com/bkeepers/dotenv).
This gem allows you to setup the environment variables your rails
application needs in order to work on your development environment.

The gem will load the environment variables from `.env` and `.ENV`
files in the application folder. To do so, you will need to call the
gem from your application.

The problem is that the gem is conceived to be used within ruby but
environment variables are an OS thing and you may need to solve the
same problem when using other platforms or languages.

Probably they have similar libraries to do it. But, **you
already have all the tools you need: your shell**.

## Exporting variables
I really like ZSH. And ZSH provides
[hooks to certain events](http://zsh.sourceforge.net/Doc/Release/Functions.html#Hook-Functions)
you can plug functions into.

One of those hooks is `chpwd`. It will run a function every time you
change your working directory. We can make use of it, and write a
simple function that checks for `.env` files in the destination folder
and sources it.

To do that we only need to write a little function and bind it to the
`chpwd` hook. That code belongs in my `.zshrc` file and looks like this:

<pre><code data-language="shell">function set_environment() {
  env_file="$PWD/.env"
  if [ -e $env_file ]; then source $env_file; fi
}
function chpwd() { set_environment; }
</code></pre>

I use `.env` files but the name doesn't really matter.

Then I create the file and export the environment variables:

    export TWITTER_KEY=''
    export TWITTER_SECRET=''
    export S3_KEY=''
    export S3_SECRET=''
    export S3_ENDPOINT='s3-eu-west-1.amazonaws.com'

And, as soon as you enter the directory where the `.env` is placed
the variables will be automatically exported and available for your
application to read.

## There are other uses
But you can do way more than exporting environment variables: you can
tailor your shell to the project you are working with.

Recently I started working on a Python project. It's my first python
project and one of my coworkers introduced me to
[virtualenv](https://pypi.python.org/pypi/virtualenv).

But, unlike RVM or rbenv, there is no such thing (as far as we know)
like `.ruby-version` files. So, I used a `.env` file to activate
the python virtual environment every time I enter the project's
folder:

    source project-virtualenv/bin/activate
    alias activate="source project-virtualenv/bin/activate"

I also used it to create an alias that allows me to have the opposite
command to the `deactivate` one provided by virtualenv (just in
case I deactivate the environment by hand).

As you see the possibilities are enormous. There are a lot of
things you can do.  Hope you find it as useful as I do!
