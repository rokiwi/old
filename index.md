---
layout: home
permalink: /
image:
  feature: main.jpg
---

<ul>
  {% for post in site.posts %}
	{% unless post.next %}
	  <h3>{{ post.date | date: '%b %Y' }}</h3>
	{% else %}
	  {% capture year %}{{ post.date | date: '%Y %b' }}{% endcapture %}
	  {% capture nyear %}{{ post.next.date | date: '%Y %b' }}{% endcapture %}
	  {% if year != nyear %}
		<h3>{{ post.date | date: '%b %Y' }}</h3>
	  {% endif %}
	{% endunless %}

	<li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
