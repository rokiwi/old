---
layout: home
permalink: /
image:
  feature: main.jpg
---

<h3>Title 1</h3>

<div class="tiles">
{% for post in site.categories.articles %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->

<h3>Title 2</h3>

<div class="tiles">
{% for post in site.categories.articles %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->
