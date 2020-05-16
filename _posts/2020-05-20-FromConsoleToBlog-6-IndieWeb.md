---
published: false
title: "Draft: From console to blog: Publishing on the IndieWeb"
tags:
 - blogging
 - unpublished
---


### h-card
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
