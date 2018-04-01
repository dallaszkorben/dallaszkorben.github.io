---
layout: category
title: Development
sidebar_link: false
---


<div class="posts">
{% for post in site.posts %}
    {% if post.blog == 'development' %}

	<div class="post">
	    <h3 class="post-title">
		<a href="{{ post.url }}">  {{ post.title }} </a>
	    </h3>
	    <div class="post-date">{{ post.date | date_to_string }}</div>
	    <br>
	</div>

    {% endif %}
{% endfor %}
</div>
