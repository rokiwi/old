---
layout: home
---

<div class="tiles">
{% for post in site.posts %}

{% if post.tags contains 'English' %}
  {% continue %}
{% endif

<article class="tile" itemscope itemtype="http://schema.org/Article">
  {% capture year %}{{ post.date | date: '%Y %b' }}{% endcapture %}
  {% capture pyear %}{{ post.next.date | date: '%Y %b' }}{% endcapture %}
  {% if year != pyear %}  
    <h2 class="post-title">{{ post.date | date: '%b %Y' }}</h2>
  {% else %}
    <div style="height: 38px;"></div>
  {% endif %}
  
  <a href="{{ site.url }}{{ post.url }}" title="{{ post.title }}" class="post-teaser">
  {% if post.image.teaser-ext %}<img src="{{ post.image.teaser-ext }}" alt="teaser" itemprop="image">
  {% else %}
    {% if post.image.teaser %}<img src="{{ site.url }}/images/{{ post.image.teaser }}" alt="teaser" itemprop="image">
      {% else %}<img src="{{ site.url }}/images/{{ site.teaser }}" alt="teaser" itemprop="image">{% endif %}
  {% endif %}
  </a>
  
  {% if post.date %}<p class="entry-date date published"><time datetime="{{ post.date | date: "%Y-%m-%d" }}" itemprop="datePublished">
  {{ post.date | date: "%B %d, %Y" }}</time></p>
  {% endif %}  
  
  {% if post.translation %}
    <a href="{% post_url /articles/2015-01-11-sue-nev-vo %}">English</a>
  {% endif %}

  <h2 class="post-title" itemprop="name"><a href="{{ site.url }}{{ post.url }}">{{ post.title }}</a></h2>
  <p class="post-excerpt" itemprop="description">{{ post.excerpt | strip_html | truncate: 160 }}</p>
</article><!-- /.tile -->
  
{% endfor %}
</div><!-- /.tiles -->

