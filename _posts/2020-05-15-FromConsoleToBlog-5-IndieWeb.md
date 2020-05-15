---
title: "From console to blog: The IndieWeb Citizenship"
tags:
 - blogging
---

Following on from the [5th part of this series](/FromConsoleToBlog-5-Tags_Categories/), let's look at [IndieWebifying blog.tomdeb.net](https://indiewebify.me/validate-rel-me/?url=https%3A%2F%2Fblog.tomdeb.net) by modifying Minimal Mistakes.

The [IndieWeb](https://indieweb.org/) is an initiative that I find interesting. 

> The IndieWeb is a community of individual personal websites, connected by simple standards, based on the principles of owning your domain, using it as your primary identity, to publish on your own site (optionally syndicate elsewhere), and own your data.

This post will focus on Level 1: Become a citizen of The IndieWeb

### Profile on home page

I first need to make sure that the author profile is included on the home page. I therefore need to modify the default _index.markdown_'s front matter as following:

index.markdown:
```md 
---
layout: home
author_profile: true
---
```

<a class="image-popup" href="/assets/images/2020-05-15-FromConsoleToBlog-5-IndieWeb/2020-05-15-FromConsoleToBlog-5-IndieWeb_1.webp"><img class="align-center" src="/assets/images/2020-05-15-FromConsoleToBlog-5-IndieWeb/2020-05-15-FromConsoleToBlog-5-IndieWeb_1-small.webp"></a>


### rel=me

The IndieWeb uses rel=me tags on hyperlink to indicate that its destination represents the same person or entity as the current page and enable things like web-sign-in. By default, Minimal Mistakes does not include rel=me tags on social links located in the sidebar. Let's address that. 

Now let's override \_includes/author-profile.html:

```sh
blog.tomdeb.net » mkdir _includes 
blog.tomdeb.net » cp ~/gems/gems/minimal-mistakes-jekyll-4.19.2/_includes/author-profile.html _includes
blog.tomdeb.net »
```

I can now edit \_includes/author-profile.html to identify the social links as rel=me.

```html
[...]
     <li><a href="{{ link.url }}" rel="me nofollow noopener noreferrer"><i class="{{ link.icon | default: 'fas fa-link' }}" aria-hidden="true"></i><span class="label">{{ link.label }}</span></a></li>
[...]
```

Add-commit-push-pull-and-build later, and blog.tomdeb.net is now a [citizen of the IndieWeb](https://indiewebify.me/validate-rel-me/?url=https%3A%2F%2Fblog.tomdeb.net).

<a class="image-popup" href="/assets/images/2020-05-15-FromConsoleToBlog-5-IndieWeb/2020-05-15-FromConsoleToBlog-5-IndieWeb_2.webp"><img class="align-center" src="/assets/images/2020-05-15-FromConsoleToBlog-5-IndieWeb/2020-05-15-FromConsoleToBlog-5-IndieWeb_2-small.webp"></a>

That's all for now. In the next post, I will look at Level 2:Publishing on the IndieWeb.
