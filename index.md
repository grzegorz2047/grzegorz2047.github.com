---
layout: page
title: Hi!
tagline: grzegorz2047 programowanie java programming language
---
{% include JB/setup %}

<br/>
{% assign post = site.posts.first %}
<a href="{{ post.url }}"></a>
<p class="blogdate">{{ post.date | date: "%d %B %Y" }}</p>
{% if post.title %}
  <h1 class="entry-title">
    <a href="{{ root_url }}{{ post.url }}">{{ post.title }}</a>
  </h1>      
{% endif %}
<div class="entry-content">{{ post.content }}</div>
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