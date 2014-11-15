---
layout: home
permalink: /
image:
  feature: main.jpg
---

{% for post in site.posts %}

{% if post.previous == false and post.next == false %}
  <h3 style="clear: both">{{ post.date | date: '%b %Y' }}</h3>
  <div class="tiles">
    {% include post-grid.html %}
  </div><!-- /.tiles -->
  {% continue %}
{% endif %}

{% if post.previous == false %}
  <h3 style="clear: both">{{ post.date | date: '%b %Y' }}</h3>
  <div class="tiles">
    {% include post-grid.html %}
  {% continue %}
{% endif %}

{% capture year %}{{ post.date | date: '%Y %b' }}{% endcapture %}
{% capture pyear %}{{ post.previous.date | date: '%Y %b' }}{% endcapture %}
{% if year != pyear %}
  </div><!-- /.tiles -->
  <h3 style="clear: both">{{ post.date | date: '%b %Y' }}</h3>
  <div class="tiles">
{% endif %}

{% include post-grid.html %}

{% if post.next == false %}
  </div><!-- /.tiles -->  
{% endif %}
  
{% endfor %}

