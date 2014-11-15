---
layout: home
permalink: /
image:
  feature: main.jpg
---

{% for post in site.posts %}

{% if forloop.first %}
  <h3 style="clear: both">{{ post.date | date: '%b %Y' }}</h3>
  <div class="tiles">    
{% endif %}

{% include post-grid.html %}

{% if forloop.last %}
  {% include post-grid.html %}
  </div><!-- /.tiles --> 
  {% continue %}  
{% endif %}

{% capture year %}{{ post.date | date: '%Y %b' }}{% endcapture %}
{% capture nyear %}{{ post.next.date | date: '%Y %b' }}{% endcapture %}
{% if year != nyear %}
  </div><!-- /.tiles -->
  <h3 style="clear: both">{{ post.date | date: '%b %Y' }}</h3>
  <div class="tiles">
{% endif %}
  
{% endfor %}

