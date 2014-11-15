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

<div class="tiles">
{% capture page-year %}{{page.date | date: "%Y"}}{% endcapture %}
{% capture page-month %}{{page.date | date: "%M"}}{% endcapture %}
<p>
{% page-year %}
</p>
{% for post in site.categories.articles %}
  {% if page-year == post-year %}
    {% include post-grid.html %}
  {% endif %}
{% endfor %}
</div><!-- /.tiles -->