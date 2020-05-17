---
title: "From console to blog: Publishing on the IndieWeb"
tags:
 - blogging
---

The objective of this post is to modify [blog.tomdeb.net](https://blog.tomdeb.net) to markup content with [microformats2](http://microformats.org/wiki/microformats-2). I will override some of Minimal Mistakes, the Jekyll them I use, to add class names to profile and content. This will hopefully allow things like cross-site comments etc ...

### h-card

First I will need to modify the author profile to add [h-card](http://microformats.org/wiki/h-card) classes:


\_includes/author-profile.html
```md
{% raw %}
<div class="h-card" itemscope itemtype="https://schema.org/Person">

  {% if author.avatar %}
    <div class="author__avatar">
      {% if author.home %}
        <a href="{{ author.home | relative_url }}">
          <img class="u-photo" src="{{ author.avatar | relative_url }}" alt="{{ author.name }}" itemprop="image">
        </a>
      {% else %}
        <img class="u-photo" src="{{ author.avatar | relative_url }}" alt="{{ author.name }}" itemprop="image">
      {% endif %}
    </div>
  {% endif %}

  <div class="author__content">
    {% if author.home %}
      <a class="u-url p-author" rel="me" href="{{ author.home }}"><h3 class="author__name" itemprop="name">{{ author.name }}</h3></a>
    {% else %}
      <h3 class="p-author author__name" itemprop="name">{{ author.name }}</h3>
    {% endif %}
    {% if author.bio %}
      <div class="p-note author__bio" itemprop="description">
        {{ author.bio | markdownify }}
      </div>
    {% endif %}
  </div>
{% endraw %}
[...]
```

The above adds h-card, u-photo, u-url, p-author and p-note to the author profile and causes the website to pass the next stage in [Indiwebification](https://indiewebify.me/validate-h-card/?url=https%3A%2F%2Fblog.tomdeb.net).


<a class="image-popup" href="/assets/images/2020-05-17-FromConsoleToBlog-6-IndieWeb/2020-05-17-FromConsoleToBlog-6-IndieWeb_0.webp"><img class="align-center" src="/assets/images/2020-05-17-FromConsoleToBlog-6-IndieWeb/2020-05-17-FromConsoleToBlog-6-IndieWeb_0-small.webp"></a>

### h-entry

Then come actual blog entries. These will need to be tagged with h-entry classes. 

```sh
 »  cp /home/tom/gems/gems/minimal-mistakes-jekyll-4.19.2/_layouts/single.html _layouts/
 »
```

```sh
blog.tomdeb.net » diff ~/gems/gems/minimal-mistakes-jekyll-4.19.2/_layouts/single.html _layouts/single.html
{% raw %}
20c20
<   <article class="page" itemscope itemtype="https://schema.org/CreativeWork">
---
>   <article class="page h-entry" itemscope itemtype="https://schema.org/CreativeWork">
29c29
<           {% if page.title %}<h1 id="page-title" class="page__title" itemprop="headline">{{ page.title | markdownify | remove: "<p>" | remove: "</p>" }}</h1>{% endif %}
---
>           {% if page.title %}<h1 id="page-title" class="page__title p-name" itemprop="headline">{{ page.title | markdownify | remove: "<p>" | remove: "</p>" }}</h1>{% endif %}
36c36
<       <section class="page__content" itemprop="text">
---
>       <section class="page__content e-content" itemprop="text">
55c55
<           <p class="page__date"><strong><i class="fas fa-fw fa-calendar-alt" aria-hidden="true"></i> {{ site.data.ui-text[site.locale].date_label | default: "Updated:" }}</strong> <time datetime="{{ page.last_modified_at | date: "%Y-%m-%d" }}">{{ page.last_modified_at | date: "%B %-d, %Y" }}</time></p>
---
>       <p class="page__date"><i class="fas fa-fw fa-calendar-alt" aria-hidden="true"></i> <a href="{{ page.url }}" class="u-url">{{ page.title | markdownify | remove: "<p>" | remove: "</p>" }}</a> was updated on <time class="dt-published" datetime="{{ page.date | date_to_xmlschema }}">{{  ege.last_modified_at| date: "%B %-d, %Y" }}</time> by <a rel="author" class="p-author h-card" href="{{ author.home }}">{{ author.name }}</a></p>
57c57
<           <p class="page__date"><strong><i class="fas fa-fw fa-calendar-alt" aria-hidden="true"></i> {{ site.data.ui-text[site.locale].date_label | default: "Updated:" }}</strong> <time datetime="{{ page.date | date_to_xmlschema }}">{{ page.date | date: "%B %-d, %Y" }}</time></p>
---
>       <p class="page__date"><i class="fas fa-fw fa-calendar-alt" aria-hidden="true"></i> <a href="{{ page.url }}" class="u-url">{{ page.title | markdownify | remove: "<p>" | remove: "</p>" }}</a> was updated on <time class="dt-published" datetime="{{ page.date | date_to_xmlschema }}">{{ page.date | date: "%B %-d, %Y" }}</time> by <a rel="author" class="p-author h-card" href="{{ author.home }}">{{ author.name }}</a></p>

{% endraw %}
```

```sh
 » cp /home/tom/gems/gems/minimal-mistakes-jekyll-4.19.2/_includes/tag-list.html _includes
 » cp /home/tom/gems/gems/minimal-mistakes-jekyll-4.19.2/_includes/category-list.html _includes
 » 
```

\_includes/category-list.html:
```md
{% raw %}
      <a href="{{ category_word | slugify | prepend: path_type | prepend: site.category_archive.path | relative_url }}" class="p-category page__taxonomy-item" rel="tag">{{ category_word }}</a>{% unless forloop.last %}<span class="sep">, </span>{% endunless %}
{% endraw %}
```


\_includes/tag-list.html:
```md
{% raw %}
      <a href="{{ tag_word | slugify | prepend: path_type | prepend: site.tag_archive.path | relative_url }}" class="p-category page__taxonomy-item" rel="tag">{{ tag_word }}</a>{% unless forloop.last %}<span class="sep">, </span>{% endunless %}
{% endraw %}
```


<figure class="half">
  <a class="image-popup" href="/assets/images/2020-05-17-FromConsoleToBlog-6-IndieWeb/2020-05-17-FromConsoleToBlog-6-IndieWeb_1.webp"><img src="/assets/images/2020-05-17-FromConsoleToBlog-6-IndieWeb/2020-05-17-FromConsoleToBlog-6-IndieWeb_1.webp"></a>
  <a class="image-popup" href="/assets/images/2020-05-17-FromConsoleToBlog-6-IndieWeb/2020-05-17-FromConsoleToBlog-6-IndieWeb_2.webp"><img src="/assets/images/2020-05-17-FromConsoleToBlog-6-IndieWeb/2020-05-17-FromConsoleToBlog-6-IndieWeb_2.webp"></a>
  <figcaption>The new single layout now complies with IndieWeb content standard.</figcaption>
</figure>

As usual, all modifications can be found on the [GitHub repository](https://github.com/tomadeb/blog.tomdeb.net).

