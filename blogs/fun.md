---
layout: page
permalink: /fun/index.html
title: Fun
tags: [my name]
imagefeature: 
chart: true
sidebar_link: true
---

<style>
hr { 
    display: block;
    margin-top: 50px;
    margin-bottom: 50px;
    margin-left: auto;
    margin-right: auto;
    border-style: inset;
    border-width: 3px;
}
</style>

<center>
    {% for image in site.static_files %}
	{% if image.path contains 'images/fun' %}

            <img src="{{ site.baseurl }}{{ image.path }}" alt="image" />
		<br>
		<hr>
		<br>
	{% endif %}
    {% endfor %}
</center>
