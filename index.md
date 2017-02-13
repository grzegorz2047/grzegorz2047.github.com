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
<h1 class="entry-title">
    <a href="{{ root_url }}{{ page.url }}">{{ page.title }}</a>
</h1>
{% if post.title %}
  <h1 class="entry-title">
    <a href="{{ root_url }}{{ post.url }}">{{ post.title }}</a>
  </h1>      
{% endif %}
<div class="entry-content">{{ content }}</div>
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