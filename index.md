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

<h1>Najnowszy post:</h1>
{% assign post = site.posts.first %}

Pozostale posty:
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>