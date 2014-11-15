---
layout: home
permalink: /
image:
  feature: main.jpg
---

{% for post in site.posts %}

{% if forloop.first and forloop.last %}
  <h3 style="clear: both">{{ post.date | date: '%b %Y' }}</h3>
  <div class="tiles">
    {% include post-grid.html %}
  </div><!-- /.tiles -->
  {% continue %}
{% endif %}

{% if forloop.first %}
  <h3 style="clear: both">{{ post.date | date: '%b %Y' }}</h3>
  <div class="tiles">
    {% include post-grid.html %}
  {% continue %}
{% endif %}


{% include post-grid.html %}

{% capture year %}{{ post.date | date: '%Y %b' }}{% endcapture %}
{% capture pyear %}{{ post.previous.date | date: '%Y %b' }}{% endcapture %}
{% if year != pyear %}
  </div><!-- /.tiles -->
  <h3 style="clear: both">{{ post.date | date: '%b %Y' }}</h3>
  <div class="tiles">
{% endif %}

{% if forloop.last %}
  </div><!-- /.tiles -->  
{% endif %}
  
{% endfor %}

