---
layout: default
---

<div class="tiles">
{% for post in site.posts %}

{% if post.tags contains 'English' %}
  {% continue %}
{% endif %}

<article class="tile" itemscope itemtype="http://schema.org/Article">

  <h2 class="post-title" itemprop="name"><a href="{{ site.url }}{{ post.url }}">{{ post.title }}</a></h2>
  <p class="post-excerpt" itemprop="description">{{ post.excerpt | strip_html | truncate: 160 }}</p>
</article><!-- /.tile -->
  
{% endfor %}
</div><!-- /.tiles -->

