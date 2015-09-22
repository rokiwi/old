---
layout: home
title: "Recettes/Recipies"
---

<ul>
{% for post in site.categories.recipes %}

<li>
  <a href="{{ site.url }}{{ post.url }}">{{ post.title }}</a>
</li>
  
{% endfor %}
</ul>


