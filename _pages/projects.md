---
layout: page
title: projects
permalink: /projects/
description: #A growing collection of your cool projects.
---



{% for project in site.projects %}

<div class="row">
	<a href="{{ BASE_PATH }}{{ project.url }}"><img class="col one" src="{{ project.thumbnail }}" style="padding-right: 50px" /></a>
  <p><a class="one" href="{{ BASE_PATH }}{{ project.url }}"><h3>{{ project.title }}</h3></a></p>
	<p>{{ project.content | strip_html | truncatewords: 40 }}</p>
</div>
<hr />
{% endfor %}