---
layout: default
---

<div>
{% for post in site.posts reversed %}

{% if post.tags contains 'English' %}
  {% continue %}
{% endif %}

{% if post.categories contains 'recipes' %}
  {% continue %}
{% endif %}

<article itemscope itemtype="http://schema.org/Article">

  <h2 class="post-title" itemprop="name">{{ post.title }}</h2>
  
  <div> {{ post.content }} </div>

</article>
  
{% endfor %}
</div>

