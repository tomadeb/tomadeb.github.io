---
title: "From console to blog: Tags & Categories"
tags:
 - blogging
---

Following on from the [4th part of this series](/FromConsoleToBlog-4-Production/), let's look at tags and categories for the content of the website. 

But first, a change from the previous posts. I am working on a post which required the example blog used so far, blog.example.com, to be accessible on the internet. Of course, I do not own example.com. example.com is one of the second-level  domains "reserved for documentation purposes and examples of the use of domain names" along with example.net, example.org, and example.edu. 

So from now on, I will be using [blog.tomdeb.net](https://blog.tomdeb.net) as the example site for this series of posts. I have also created a new Git repository on Github for it, [tomadeb/blog.tomdeb.net](https://github.com/tomadeb/blog.tomdeb.net). 

Back to tags and categories. By default, Jekyll and MinimalMistakes' support for tags and categories is insufficient. 

Content can be tagged and/or categorised,
       
<a class="image-popup" href="/assets/images/2020-05-13-FromConsoleToBlog-5-Tags_Categories/2020-05-13-FromConsoleToBlog-5-Tags_Categories_1.webp">
  <img class="align-center" src="/assets/images/2020-05-13-FromConsoleToBlog-5-Tags_Categories/2020-05-13-FromConsoleToBlog-5-Tags_Categories_1_small.webp">
</a>

... but content indexing by tag or category does not work. 

<a class="image-popup" href="/assets/images/2020-05-13-FromConsoleToBlog-5-Tags_Categories/2020-05-13-FromConsoleToBlog-5-Tags_Categories_2.webp">
  <img class="align-center" src="/assets/images/2020-05-13-FromConsoleToBlog-5-Tags_Categories/2020-05-13-FromConsoleToBlog-5-Tags_Categories_2_small.webp">
</a>

Thankfully, this can be addressed very quickly.

First, a Jekyll-plugin is necessary. Jekyll-archives will generate archive pages based on groups and patterns defined in the configuration.

/home/user1/blog.tomdeb.net/Gemfile:
```conf
[...]
group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.12"
  [...]
  gem "jekyll-archives"
end
[...]
```

Then I can use bundle to install the gem:
```shell
➜  blog.tomdeb.net git:(master) ✗ bundle
[...]
Using jekyll-archives 2.2.1
[...]
Bundle complete! 13 Gemfile dependencies, 51 gems now installed.
Use `bundle info [gemname]` to see where a bundled gem is installed.
➜  blog.tomdeb.net git:(master) ✗ 
```

Finally, I can activate it in \_config.

/home/user1/blog.tomdeb.net/\_config:
```conf

# Plugins (previously gems:)
[...]
plugins:
  - jekyll-paginate
  - jekyll-sitemap
  - jekyll-gist
  - jekyll-feed
  - jemoji
  - jekyll-include-cache
  - jekyll-archives

[...]

# Archives
#  Type
#  - GitHub Pages compatible archive pages built with Liquid ~> type: liquid (default)
#  - Jekyll Archives plugin archive pages ~> type: jekyll-archives
#  Path (examples)
#  - Archive page should exist at path when using Liquid method or you can
#    expect broken links (especially with breadcrumbs enabled)
#  - <base_path>/tags/my-awesome-tag/index.html ~> path: /tags/
#  - <base_path/categories/my-awesome-category/index.html ~> path: /categories/
#  - <base_path/my-awesome-category/index.html ~> path: /
category_archive:
  type: jekyll-archives
  path: /categories/
tag_archive:
  type: jekyll-archives
  path: /tags/
# https://github.com/jekyll/jekyll-archives
jekyll-archives:
  enabled:
    - categories
    - tags
  layouts:
    category: archive-taxonomy
    tag: archive-taxonomy
  permalinks:
    category: /categories/:name/
    tag: /tags/:name/

[...]
```
Regenerate your site and BOOM, I have now posts indexed by tag and categories.

<a class="image-popup" href="/assets/images/2020-05-13-FromConsoleToBlog-5-Tags_Categories/2020-05-13-FromConsoleToBlog-5-Tags_Categories_3.webp">
  <img class="align-center" src="/assets/images/2020-05-13-FromConsoleToBlog-5-Tags_Categories/2020-05-13-FromConsoleToBlog-5-Tags_Categories_3_small.webp">
</a>


