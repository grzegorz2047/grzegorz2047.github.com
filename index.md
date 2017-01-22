---
layout: page
title: Witaj!
tagline: grzegorz2047 programowanie java
---
{% include JB/setup %}
{% include JB/posts_collate %}

Fajny kod:

	System.out.println("elo");

Aktualne posty:
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
	
  {% endfor %}
</ul>