---
layout: default
---

<div class="tiles">
{% for post in site.posts %}

{% if post.tags contains 'English' %}
  {% continue %}
{% endif %}

<article class="tile" itemscope itemtype="http://schema.org/Article">

  <h2 class="post-title" itemprop="name"></h2>
  
  <div> {{ post.content }} </div>

</article><!-- /.tile -->
  
{% endfor %}
</div><!-- /.tiles -->

