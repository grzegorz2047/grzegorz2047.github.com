---
layout: page
title: Witaj!
tagline: grzegorz2047 programowanie java
---
{% include JB/setup %}
{% include JB/posts_collate %}

Fajny kod:

	System.out.println("elo");

{% highlight java %}
public class FajnaKlasa {
	public static main(String[] args) {
		System.out.println("Witaj na mojej stronie!");
	}
}
{% endhighlight %}
===================================
<br/>
{% assign post = site.posts.first %}
<a href="{{ post.url }}">
<h3>{{ post.title }}</h3>
<p class="blogdate">{{ post.date | date: "%d %B %Y" }}</p>
<div>{{ post.content |truncatehtml | truncatewords: 60 }}</div>
</a>
<br/>
Lista postów:
<ul>
{% for post in site.posts %}
<li>
  <a href="{{ post.url }}">{{ post.title }}</a>
  {{ post.excerpt }}
</li>
{% endfor %}
</ul>