---
layout: home
title: "Test"
---

<div class="tiles">
{% for post in site.posts %}

<article class="tile" itemscope itemtype="http://schema.org/Article">
  <h2 class="post-title" itemprop="name"><a href="{{ site.url }}{{ post.url }}">{{ post.title }}</a></h2>
</article>
  
{% endfor %}
</div><!-- /.tiles -->


