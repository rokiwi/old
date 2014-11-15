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

	<article>
	  <a href="{{ site.url }}{{ post.url }}" title="{{ post.title }}" class="post-teaser">{% if post.image.teaser %}<img src="{{ site.url }}/images/{{ post.image.teaser }}" alt="teaser" itemprop="image">
		{% else %}<img src="{{ site.url }}/images/{{ site.teaser }}" alt="teaser" itemprop="image">{% endif %}</a>
	  {% if post.date %}<p class="entry-date date published"><time datetime="{{ post.date | date: "%Y-%m-%d" }}" itemprop="datePublished">{{ post.date | date: "%B %d, %Y" }}</time></p>{% endif %}
	  <h2 class="post-title" itemprop="name"><a href="{{ site.url }}{{ post.url }}">{{ post.title }}</a></h2>
	  <p class="post-excerpt" itemprop="description">{{ post.excerpt | strip_html | truncate: 160 }}</p>
	</article>
	
  {% endfor %}
</ul>



