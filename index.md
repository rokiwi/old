---
layout: home
permalink: /
image:
  feature: main.jpg
---

<div class="tiles">
{% for post in site.posts %}

<article class="tile" itemscope itemtype="http://schema.org/Article">
  <a href="{{ site.url }}{{ post.url }}" title="{{ post.title }}" class="post-teaser">
  {% if post.image.teaser %}<img src="{{ site.url }}/images/{{ post.image.teaser }}" alt="teaser" itemprop="image">
    {% else %}<img src="{{ site.url }}/images/{{ site.teaser }}" alt="teaser" itemprop="image">{% endif %}</a>
  {% if post.date %}<p class="entry-date date published"><time datetime="{{ post.date | date: "%Y-%m-%d" }}" itemprop="datePublished">
  {{ post.date | date: "%B %d, %Y" }}</time></p>
  {% endif %}
  
    {% capture year %}{{ post.date | date: '%Y %b' }}{% endcapture %}
	{% capture pyear %}{{ post.previous.date | date: '%Y %b' }}{% endcapture %}
	{% if year != pyear %}
	  
	  <h2 class="post-title">{{ post.previous.date | date: '%b %Y' }}</h3>

	{% endif %}
  
  <h2 class="post-title" itemprop="name"><a href="{{ site.url }}{{ post.url }}">{{ post.title }}</a></h2>
  <p class="post-excerpt" itemprop="description">{{ post.excerpt | strip_html | truncate: 160 }}</p>
</article><!-- /.tile -->

  
{% endfor %}
</div><!-- /.tiles -->

