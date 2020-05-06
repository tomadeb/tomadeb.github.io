---
title: 'From console to blog: Jekyll'
tags:
 - blogging
---

Following on from [yesterday's introductory post]({% link _posts/2020-05-04-FromConsoleToBlog-0-Intro.md %}), I will now go through the process of creating a development environment for our website. 

### Installing the requirements 

Let's make sure the [Debian](https://debian.org) machine I am using is fully up to date.

```shell
> sudo apt update && sudo apt -y upgrade
> sudo reboot
```

Install Ruby and development tools
```shell
> sudo apt -y install build-essential make ruby ruby-dev
...
>
```

I now need to amend my user environment to configure Ruby where to store gems:

```shell
> vim .zshrc
...
export GEM_HOME=$HOME/gems
export PATH=$HOME/gems/bin:$PATH
...
:wq
> source ~/.zshrc
```

### Install Jekyll


#### First, Bundler


From [blunder.io](https://bundler.io/):
> Bundler provides a consistent environment for Ruby projects by tracking and installing the exact gems and versions that are needed.
Bundler is an exit from dependency hell, and ensures that the gems you need are present in development, staging, and production. Starting work on a project is as simple as bundle install.

```shell
> gem install bundler
Fetching: bundler-2.1.4.gem (100%)
Successfully installed bundler-2.1.4
Parsing documentation for bundler-2.1.4
Installing ri documentation for bundler-2.1.4
Done installing documentation for bundler after 3 seconds
1 gem installed
>
```

#### Then, Jekyll:

```shell
> gem install jekyll
...
Done installing documentation for public_suffix, addressable, colorator, http_parser.rb, eventmachine, em-websocket, concurrent-ruby, i18n, ffi, sassc, jekyll-sass-converter, rb-fsevent, rb-inotify, listen, jekyll-watch, rexml, kramdown, kramdown-parser-gfm, liquid, mercenary, forwardable-extended, pathutil, rouge, safe_yaml, unicode-display_width, terminal-table, jekyll after 27 seconds
27 gems installed
```

#### Create a new Jekyll site

```shell
> jekyll new blog.example.com
...
  Bundler: Bundle complete! 6 Gemfile dependencies, 31 gems now installed.
  Bundler: Use `bundle info [gemname]` to see where a bundled gem is installed.
New jekyll site installed in /home/user/blog.example.com.
>
```

#### Starting Jekyll

```shell
> bundle exec jekyll serve --host 127.0.0.1 -l 
Configuration file: /Users/user/blog.example.com/_config.yml
            Source: /Users/user/blog.example.com
       Destination: /Users/user/blog.example.com/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
       Jekyll Feed: Generating feed for posts
                    done in 0.399 seconds.
 Auto-regeneration: enabled for '/Users/user/blog.example.com'
LiveReload address: http://127.0.0.1:35729
    Server address: http://127.0.0.1:4000//
  Server running... press ctrl-c to stop.
        LiveReload: Browser connected
```

You can now point your browser at http://127.0.0.1:4000/:

![Vanilla Jekyll]({{ site.url }}{{ site.baseurl }}/assets/images/20200505-jekyll1.webp){: .full}

![Welcome to Jekyll!]({{ site.url }}{{ site.baseurl }}/assets/images/20200505-jekyll2.webp){: .full}

That's it for now. In the next post, I'll go through how to use [a Jekyll theme I quite like](https://mmistakes.github.io/minimal-mistakes/). 
