---
layout: home
permalink: /
image:
  feature: main.jpg
---

{% for post in site.posts %}
{% unless post.next %}
  <h3 style="clear: both">{{ post.date | date: '%b %Y' }}</h3>
  <div class="tiles">
{% else %}
  {% capture year %}{{ post.date | date: '%Y %b' }}{% endcapture %}
  {% capture nyear %}{{ post.next.date | date: '%Y %b' }}{% endcapture %}
  {% if year != nyear %}
    </div><!-- /.tiles -->
	<h3 style="clear: both">{{ post.date | date: '%b %Y' }}</h3>
	<div class="tiles">
  {% endif %}
{% endunless %}
  {% include post-grid.html %}
  
{% endfor %}
</div><!-- /.tiles -->
