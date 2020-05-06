---
title: 'From console to blog: Introduction'
tags:
 - blogging
---

I disagree with [KevQ](https://kevq.uk/which-wordpress-plugins-i-use/) on this one, I don't think running WordPress is a good idea. 

I don't really like the idea of running my own instance of any Content Management Systems (CMS) like [Drupal](https://www.drupal.org/), [WordPress](https://wordpress.com/) or [Joomla](https://www.joomla.org/). I used to be a really big fan of Drupal for quite a while, particularly when it introduced [the hook system](https://api.drupal.org/api/drupal/includes!module.inc/group/hooks/5.x). I thought it was really clever stuff and made - and I'm sure still makes - for a very adaptable CMS. I even got involved in running its french community at some point.

But then a [series](https://www.drupal.org/node/2146839) of [disastrous](https://www.drupal.org/sa-core-2018-004) [vulnerabilities](https://www.drupal.org/sa-core-2019-003) pushed me away from it. 

To me, the main problem with CMS is size. The amount of code required to provide performance, flexibility and accessibility is just too significant and creates too many opportunities for vulnerabilities. I don't like the idea of a website having authentication, an admin interface, an editor or a file uploader, among other things. When I create or choose tools to use, I always try to stick to the Unix Philosophy. I like to use minimalist tools which do one thing and do it well. I also try, whenever possible, to reuse the tools that I know. I have been using a particular text editor for more than 20 years and will always prefer using it. I know ssh is a secure protocol and I know how to configure it securely. I prefer using this as an admin interface and file uploader. 

So here we go, I have tried to convince you that running your own CMS instance is not necessarily a good idea. Now what then?!? What are the other options?  Building a website from scratch can be fun, but let's not reinvent the wheel and find an acceptable compromise between features and security. The (relatively) new kid on the block when it comes to running small websites is to use a static site generator. It allows its users to generate static HTML pages from plain text files. Once generated, the HTML files are served as static files by a web server software such as Apache HTTPD or Nginx, and do not require any server side scripting. 

The 800-pound gorilla of static site generators is [Jekyll](https://jekyllrb.com/). From [their website](https://jekyllrb.com/docs/): 
> Jekyll is a static site generator. You give it text written in your favorite markup language and it uses layouts to create a static website. You can tweak how you want the site URLs to look, what data gets displayed on the site, and more.

In this series of posts, I will attempt to detail the process of getting a small, personal website running from the console. I will go through the process of installation, basic visual tweaks and security configuration. I'll then explain how using the console allows for a lot of automation and hopefully by the end of it, you might not even need to logon to your server anymore.  [Debian](https://debian.org) is my Linux distribution of choice. I have been using Linux for a very long time and I think Debian is the best distribution out there for [a](https://www.debian.org/doc/manuals/project-history/manifesto.en.html)  [number](https://wiki.debian.org/DebianPackageManagement)  [of](https://www.debian.org/devel/debian-installer/)  [reasons](https://www.debian.org/distrib/packages). These instructions may occasionnally be specific to Debian, but can easily be applied to other Linux distributions or operating systems.

So with baited breath, here it is, [From Console to Blog - 1 - Jekyll]() 
