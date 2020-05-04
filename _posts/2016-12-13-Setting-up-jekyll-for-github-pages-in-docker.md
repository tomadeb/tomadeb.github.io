---
title: Setting Jekyll for Github Pages in Docker
tags:
  - blogging
---

According to [Jekyll's website](https://jekyllrb.com/docs/home/):

> Jekyll is a simple, blog-aware, static site generator. It takes a template directory containing raw text files in various formats, runs it through a converter (like [Markdown](https://daringfireball.net/projects/markdown/)) and our [Liquid](https://github.com/Shopify/liquid/wiki) renderer, and spits out a complete, ready-to-publish static website suitable for serving with your favorite web server. Jekyll also happens to be the engine behind [GitHub Pages](https://pages.github.com/), which means you can use Jekyll to host your project’s page, blog, or website from GitHub’s servers for free.

The reason why Jekyll works so well with Github is that all of the content's website is stored in raw text files which can then be version controlled on Github. You then manage your website's content exactly the same way you manage your development code. Pretty Good Stuff !

I thing that, in my previous attempts at blogging, I got b(l)ogged down (...) too much on the technical details of the blog: the server, the hosting, the CMS, database, content types etc. This time around, I want to focus almost exclusively on the content. With Jekyll and Github Pages, I had a hosted site that more or less fit the bill, and a complete dev environment on my home server in approximately 5 hours. And here is what I did during that time:  

## Github Repo for the live site

The first thing was to create a Github repository for the website. After a little research, I found [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) and decided the clear and simple design was a good start. So I followed the [documentation](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/), forked the Minimal Mistakes Theme and renamed it accordingly to [tomadeb.github.io](https://github.com/tomadeb/tomadeb.github.io). [tomadeb.github.io](https://tomadeb.github.io) became a copy of the Minimal Mistakes live demo website. All I needed to do now was to customise it slightly by modifying _Config.yml and cleaning up the repository:

{% highlight shell %}
~ > git clone https://github.com/tomadeb/tomadeb.github.io.git
...
~ > cd tomadeb.github.io
...
~/tomadeb.github.io > git rm -r docs test screenshot-layouts.png screenshot.png
...
~/tomadeb.github.io > git push origin --delete gh-pages-3.1.6
...
~/tomadeb.github.io > git push origin --delete gh-pages-2.2.1
...
~/tomadeb.github.io > git push origin --delete develop
...
~/tomadeb.github.io > echo "" > README.md
...
~/tomadeb.github.io > vim _Config.yml
...
~/tomadeb.github.io > git commit -a -m 'first basic tweaks' 
...
~/tomadeb.github.io > git push
...
{% endhighlight %}

Yes. That was all I needed to do to ge the first version of the blog. Now, what I needed was a development environment on my home server.

## Development environment

### Create Jekyll docker image 

I wanted the dev environment to be as portable as possible, so I tried to use the [jekyll/jekyll]() docker image but with no luck. Gems required by the theme would not install. I had to create a bespoke image which would contain everything I needed.

The image was created via a [Dockerfile](https://docs.docker.com/engine/reference/builder/):

```
FROM ubuntu
RUN apt update && apt -y upgrade && apt -y install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev rubygems ruby-dev
RUN mkdir -p /srv/jekyll
RUN gem install jekyll bundler
COPY Gemfile /root
COPY jekyll.gemspec /root
RUN cd /root && bundle install
EXPOSE 4000
WORKDIR /srv/jekyll
```

This Dockerfile will duplicate the ubuntu image and install all the software required for jekyl and its theme, as well as jekyll itself. 

The build is initiated with:

{% highlight sh %}
/h/t/W/m/jekyll > sudo docker build -t tomdeb/jekyll . 
...
{% endhighlight %}

The *tomdeb/jekyll* image should now be available to use:

{% highlight sh %}
/h/t/W/m/jekyll > sudo docker images 
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
...
tomdeb/jekyll       latest              abababababab        -----------         672.5 MB
...
{% endhighlight %}

We can now create a docker-compose file to make use of the above image and create a container for the dev environment.

### Create docker-compose file

The docker-compose file *docker-compose.yml* contains the follwoing:

```
version: '2'

services:
  jekyll:
    image: tomdeb/jekyll
    command: jekyll serve -watch --future --host jekyll
    ports:
      - 4000:4000
    volumes:
      - /home/tom/tomadeb.github.io:/srv/jekyll
```

The container is then created with the following command:

{% highlight sh %}
/h/t/W/m/jekyll > sudo docker-compose up
Creating jekyll_jekyll_1
Attaching to jekyll_jekyll_1
jekyll_1  | Configuration file: /srv/jekyll/_config.yml
jekyll_1  | Configuration file: /srv/jekyll/_config.yml
jekyll_1  |             Source: /srv/jekyll
jekyll_1  |        Destination: /srv/jekyll/_site
jekyll_1  |  Incremental build: disabled. Enable with --incremental
jekyll_1  |       Generating...
jekyll_1  |                     done in 2.599 seconds.
jekyll_1  |  Auto-regeneration: enabled for '/srv/jekyll'
jekyll_1  | Configuration file: /srv/jekyll/_config.yml
jekyll_1  |     Server address: http://jekyll:4000/
jekyll_1  |   Server running... press ctrl-c to stop.
{% endhighlight %}

As we can see from the output, a container named *jekyll_jekyll_1* has been created. The folder */home/tom/tomadeb.github.io* has been mapped to */srv/jekyll* and port *40000/tcp* has been natted on the docker host to port *4000/tcp* on the container.

```
/h/t/W/m/jekyll > sudo docker ps
[sudo] password for tom:
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                    NAMES
cfaa7df2e890        tomdeb/jekyll       "jekyll serve --watch"   6 minutes ago       Up 6 minutes        0.0.0.0:4000->4000/tcp   jekyll_jekyll_1
```
I can now access my Jekyll dev environment at:

*http://\<docker-host.fqdn\>:4000/*.


Note: Everything documented here is [available on github](https://github.com/tomadeb/W/tree/master/myapp/docker/jekyll).
