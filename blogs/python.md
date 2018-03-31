---
layout: default
title: Python
sidebar_link: false
---


{{ paginator }}


<div class="posts">
{% for post in site.posts %}
    {% if post.blog == 'python' %}

	<div class="post">
	    <h3 class="post-title">
		<a href="{{ post.url }}">  {{ post.title }} </a>
	    </h3>
	    <span class="post-date">{{ post.date | date_to_string }}</span>
	    <br>
	</div>

    {% endif %}
{% endfor %}
</div>
