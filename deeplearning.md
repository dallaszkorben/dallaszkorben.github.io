---
layout: page
title: Deep Learning
sidebar_link: true
---

<div class="posts">
{% for post in site.posts %}
    {% if post.blog == 'deeplearning' %}

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
