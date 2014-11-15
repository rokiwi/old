---
layout: home
permalink: /

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

{% if forloop.first %}
  {% continue %}  
{% endif %}

{% capture year %}{{ post.date | date: '%Y %b' }}{% endcapture %}
{% capture pyear %}{{ post.previous.date | date: '%Y %b' }}{% endcapture %}
{% if year != pyear %}
  </div><!-- /.tiles -->
  <h3 style="clear: both">{{ post.previous.date | date: '%b %Y' }}</h3>
  <div class="tiles">
{% endif %}
  
{% endfor %}

