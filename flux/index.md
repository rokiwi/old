-----
layout: home
----

{% for post in site.posts %}

{% if post.tags contains 'English' %}
  {% continue %}
{% endif %}

	<article>
		<div class="page-title">
			<h1>{{ post.title }}</h1>
		</div>
		<div class="inner-wrap">
			<div id="content" class="page-content" itemprop="articleBody">
				{{ post.content }}
				<hr />
			</div><!-- /.content -->
		</div><!-- /.inner-wrap -->
	</article><!-- ./wrap -->
{% endfor %}
