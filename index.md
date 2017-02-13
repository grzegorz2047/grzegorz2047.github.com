---
layout: page
title: Hi!
tagline: grzegorz2047 programowanie java programming language
---
{% include JB/setup %}

<br/>
{% assign post = site.posts.first %}
<a href="{{ post.url }}"></a>
<h3>{{ post.title }}</h3>
<p class="blogdate">{{ post.date | date: "%d %B %Y" }}</p>
<div>
	{{ post.content |truncatehtml | truncatewords: 60 }}
</div>
<br/>
My posts:
<ul>
{% for post in site.posts %}
<li>
  <a href="{{ post.url }}">{{ post.title }}</a>
  {{ post.excerpt }}
</li>
{% endfor %}
</ul>