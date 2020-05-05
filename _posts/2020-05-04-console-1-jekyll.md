---
title: 'From console to blog: introduction'
tags:
 - blogging
---

I disagree with [KevQ](https://kevq.uk/which-wordpress-plugins-i-use/) on this one, I don't think running WordPress is a good idea. 

I don't really like the idea of running my own instance of any Content Management Systems (CMS) like [Drupal](https://www.drupal.org/), [WordPress](https://wordpress.com/) or [Joomla](https://www.joomla.org/). I used to be a really big fan of Drupal for quite a while, particularly when it introduced [the hook system](https://api.drupal.org/api/drupal/includes!module.inc/group/hooks/5.x). I thought it was really clever stuff and made - and I'm sure still makes - for a very adaptable CMS. I even got involved in running its french community at some point.

But then a [series](https://www.drupal.org/node/2146839) of [disastrous](https://www.drupal.org/sa-core-2018-004) [vulnerabilities](https://www.drupal.org/sa-core-2019-003) pushed me away from it. 

To me, the main problem with CMS is size. The amount of code required to provide performance, flexibility and accessibility is just too significant and creates too many opportunities for vulnerabilities. I don't like the idea of a website having authentication, an admin interface, an editor or a file uploader, among other things. When I create or choose tools to use, I always try to stick to the Unix Philosophy. I like to use minimalist tools which do one thing and do it well. I also try, whenever possible, to reuse the tools that I know. I have been using a particular text editor for more than 20 years and will always prefer using it. I know ssh is a secure protocol and I know how to configure it securely. I prefer using this as an admin interface and file uploader. 

So here we go, I have tried to convince you that running your own CMS instance is not necessarily a good idea. Now what then?!? Building a website from scratch can be fun, but let's not reinvent the wheel and find an acceptable compromise between features and security.

In this series of posts, I will attempt to detail the process of getting a small, personal website running from the console. I will go through the process of installation, basic visual tweaks and security configuration. I'll then explain how using the console allows for a lot of automation and hopefully by the end of it, you might not even need to logon to your server anymore. 

I take a few assumptions along the way. I assume that one is reasonably familiar with the Linux console. I also assume that you have the following already:
- a debian linux server
- root access to said server
- a domain name
- a DNS A record pointing at the server's IP address.

Debian is my Linux distribution of choice. I have been using Linux for a very long time and I think Debian is the best distribution out there for a number of reasons. To name but a few: [The Debian Manifesto](https://www.debian.org/doc/manuals/project-history/manifesto.en.html), [dpkg and apti](https://wiki.debian.org/DebianPackageManagement), [debian-installer](https://www.debian.org/devel/debian-installer/) and [the sheer number of packages available](https://www.debian.org/distrib/packages). 

### Static Site Generators

The (relatively) new kids on the block when it comes to running small websites are static Site Generators. These allow you generate static HTML pages from plain text files. Once generated, these HTML are served as-is to the visitor and do not require any additional dynamic content generation server side.  

The 800-pound gorilla of static site generators is [Jekyll](https://jekyllrb.com/). From [their website](https://jekyllrb.com/docs/): 
> Jekyll is a static site generator. You give it text written in your favorite markup language and it uses layouts to create a static website. You can tweak how you want the site URLs to look, what data gets displayed on the site, and more.

### Installing the requirements 

Let's make sure we are fully up to date.

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

Amend user environment to configure Ruby where to store gems:

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

```shell
> gem install jekyll
...
Done installing documentation for public_suffix, addressable, colorator, http_parser.rb, eventmachine, em-websocket, concurrent-ruby, i18n, ffi, sassc, jekyll-sass-converter, rb-fsevent, rb-inotify, listen, jekyll-watch, rexml, kramdown, kramdown-parser-gfm, liquid, mercenary, forwardable-extended, pathutil, rouge, safe_yaml, unicode-display_width, terminal-table, jekyll after 27 seconds
27 gems installed
```

### Create a new Jekyll site

```shell
> jekyll new blog.example.com
...
  Bundler: Bundle complete! 6 Gemfile dependencies, 31 gems now installed.
  Bundler: Use `bundle info [gemname]` to see where a bundled gem is installed.
New jekyll site installed in /home/user/blog.example.com.
>
```

### Starting Jekyll

```shell
> bundle exec jekyll serve
```

You can now point your browser at http://\<ip.ad.re.ss\>:4000/:

![Vanilla Jekyll]({{ site.url }}{{ site.baseurl }}/assets/images/20200505-jekyll1.png){: .full}

![Welcome to Jekyll!]({{ site.url }}{{ site.baseurl }}/assets/images/20200505-jekyll2.png){: .full}

That's it for now. In the next post, I'll go through how to add a TLS certificate and configure Nginx as a reverse proxy for your new Jekyll site. 
