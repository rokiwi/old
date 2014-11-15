---
layout: archive
title: "Articles"
date: 2014-05-30T11:39:03-04:00
modified:
tags: []
image:
  feature:
  teaser:
---
<ul>
  {% for post in site.categories.articles %}
	{% unless post.next %}
	  <h3>{{ post.date | date: '%Y %b' }}</h3>
	{% else %}
	  {% capture year %}{{ post.date | date: '%Y %b' }}{% endcapture %}
	  {% capture nyear %}{{ post.next.date | date: '%Y %b' }}{% endcapture %}
	  {% if year != nyear %}
		<h3>{{ post.date | date: '%Y %b' }}</h3>
	  {% endif %}
	{% endunless %}

	<div class="tiles">
	  {% include post-grid.html %}
	</div>
  {% endfor %}
</ul>



