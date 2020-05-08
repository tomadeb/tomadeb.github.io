---
title: 'From console to blog: Minimal Mistakes'
tags:
 - blogging
---

Following on from [yesterday's post]({% link _posts/2020-05-05-FromConsoleToBlog-1-Jekyll.md %}) on installing [Jekyll](https://jekyllrb.com), I will now go through the process of installing and customising the [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) theme. 

### Installing Minimal Mistakes
* install the gem:

```shell
➜  blog.example.com > echo "gem \"minimal-mistakes-jekyll\"" >> Gemfile 
➜  blog.example.com > bundle
...
Bundle complete! 13 Gemfile dependencies, 51 gems now installed.
Use `bundle info [gemname]` to see where a bundled gem is installed.
➜  blog.example.com >
```
* Download the default config file and pagniation index file:

```shell
➜  blog.example.com > curl -s -O https://raw.githubusercontent.com/mmistakes/minimal-mistakes/master/_config.yml
➜  blog.example.com > curl -s -O https://raw.githubusercontent.com/mmistakes/minimal-mistakes/master/index.html
➜  blog.example.com >
```
* Enable the theme:

```shell
➜  blog.example.com > perl -p -i -e 's/#\s+theme/theme/' _config.yml
➜  blog.example.com >
```
* fix the layouts of Jekyll's sample post and page:

```shell
➜  blog.example.com > perl -p -i -e  's/layout: post//' _posts/2020-05-07-welcome-to-jekyll.markdown
➜  blog.example.com > perl -p -i -e  's/layout: page/layout: single/' about.markdown
➜  blog.example.com >
```

<figure class="half">
  <a class="image-popup" href="/assets/images/2020-05-06-FromConsoleToBlog-2-MinimalMistakes/2020-05-06-FromConsoleToBlog-2-MinimalMistakes_2.webp"><img src="/assets/images/2020-05-06-FromConsoleToBlog-2-MinimalMistakes/2020-05-06-FromConsoleToBlog-2-MinimalMistakes_2.webp"></a>
  <a class="image-popup" href="/assets/images/2020-05-06-FromConsoleToBlog-2-MinimalMistakes/2020-05-06-FromConsoleToBlog-2-MinimalMistakes_1.webp"><img src="/assets/images/2020-05-06-FromConsoleToBlog-2-MinimalMistakes/2020-05-06-FromConsoleToBlog-2-MinimalMistakes_1.webp"></a>
  <figcaption>Vanilla Minimal Mistakes.</figcaption>
</figure>


### Configuring Minimal Mistakes

Configuration is in \_config.yml and is rather self-explanatory and its [official documentation](https://mmistakes.github.io/minimal-mistakes/docs/configuration/) is good. 

### Basic design tweaks 

Most of us will want to make CSS basic design changes to minimal mistakes and/or the chosen theme. 

* Create folders for local css files:

```shell
➜  blog.example.com > mkdir -p assets/css _sass
➜  blog.example.com >
```
* Copy default main.css from gem:

```shell
➜  blog.example.com > cp ~/gems/gems/minimal-mistakes-jekyll-*/assets/css/main.scss assets/css/
➜  blog.example.com >
```
* Add entries for blog and highlight css:

```shell
➜  blog.example.com > echo "@import \"blog\";" >> assets/css/main.scss
➜  blog.example.com > echo "@import \"syntaxhighlight\";" >> assets/css/main.scss
➜  blog.example.com >
```
* Create empty blog css file:

```shell
➜  blog.example.com > touch _sass/blog.scss
➜  blog.example.com >
```
Override CSS can now be added to \_sass/blog.scss which will be importe dby main.scss


* Generate css file for the code syntax highlighter, Rougify:

```shell
➜  blog.example.com > rougify style colorful > _sass/syntaxhighlight.scss
➜  blog.example.com > 
```
* Restart Jekyll:

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

<figure class="half">
  <a class="image-popup" href="/assets/images/2020-05-06-FromConsoleToBlog-2-MinimalMistakes/2020-05-06-FromConsoleToBlog-2-MinimalMistakes_2.webp"><img src="/assets/images/2020-05-06-FromConsoleToBlog-2-MinimalMistakes/2020-05-06-FromConsoleToBlog-2-MinimalMistakes_2.webp"></a>
  <a class="image-popup" href="/assets/images/2020-05-06-FromConsoleToBlog-2-MinimalMistakes/2020-05-06-FromConsoleToBlog-2-MinimalMistakes_3.webp"><img src="/assets/images/2020-05-06-FromConsoleToBlog-2-MinimalMistakes/2020-05-06-FromConsoleToBlog-2-MinimalMistakes_3.webp"></a>
  <figcaption>Vanilla Minimal Mistakes.</figcaption>
</figure>


