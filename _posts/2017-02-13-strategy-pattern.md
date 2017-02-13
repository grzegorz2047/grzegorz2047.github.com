---
layout: post
title: "Strategy pattern in Java"
description: "Here is something about stategy pattern"
category: java patterns
tags: []
---
{% include JB/setup %}

<br/>
Hi, some time ago I started learning about java design patterns because as a java developer
I should have some knowledge about how to create good java application.<br/>
In java, people use different patterns to help create good code.<br/>
For example we have GRASP patterns, SOLID patterns and much more.<br/>
In this post I'm going to describe strategy pattern. The reason is simple. <br/>
Firstly, I'd like to memorize it, secondly, in case when I forget it I'd like to go back and look at it.<br/>
Also maybe someone will learn something new if someone have never heard about design patterns.<br/>
So, when do we use strategy pattern?<br/>
We use it when we have to implement different algorithms which are used interchangeably.<br/>
So for example, when we have different types of discounts, how should we implement it?<br/>
Let's say, that we have a shop and we want to give 20% discount for our products to all students.<br/>
We can create class Product:<br/>

{% highlight java %}
public class Product {
	
	private String name;
	private BigDecimal price;

	public Product(String name, BigDecimal price) {
		this.name = name;
		this.price = price;
	}
}
{% endhighlight %} 

Let's stop for a second and think, how beginner java programmer would implement it?<br/>
He would probably think, that Product can compute discount for himself.<br/>
It would look like something like that:<br/>

{% highlight java %}
public class Product {
	
	private String name;
	private BigDecimal price;

	public Product(String name, BigDecimal price) {
		this.name = name;
		this.price = price;
	}
	
	public String computeDiscount(String discountName) {
		if(discountName == "student") {
			return String.valueOf(price + (price * 20)/100);
		}
		if(discountName == "newclient") {
			return price + String.valueOf((price * 10)/100);
		}
	}
}
{% endhighlight %} 

What if we want to implement discounts for 10 or even more types of people?<br/>
Then, in this case, we add more if's!<br/>
Well, that would work, but it's not really good idea.<br/>
So in this case, we can use Strategy pattern.<br/>
So basically we will provide for our Product Discount interface, so when we will be computing<br/>
discount, we simply give specific algorithm, which gives us appropriate discount.<br/>
To do this, let's create an interface called Discount:<br/>

{% highlight java %}
public interface Discount {
	
	BigDecimal compute(BigDecimal price);

}
{% endhighlight %} 
 
Now, let's implement it to for our student discount:<br/>

{% highlight java %}
public class StudentDiscount implements Discount {
	
	public BigDecimal compute(BigDecimal price) {
		BigDecimal discount = new BigDecimal("0.8");
		return price.multiply(discount);
	}
}
{% endhighlight %} 

and for new client discount:<br/>

{% highlight java %}
public class NewClientDiscount implements Discount {
	
	public BigDecimal compute(BigDecimal price) {
		BigDecimal discount = new BigDecimal("0.9");
		return price.multiply(discount);
	}
}
{% endhighlight %} 

Let's apply it to our Product class:<br/>

{% highlight java %}
public class Product {
	
	private String name;
	private BigDecimal price;
	private Discount discountStrategy;

	public Product(String name, BigDecimal price) {
		this.name = name;
		this.price = price;
	}
	
	public BigDecimal computePrice() {
		return discountStrategy.compute(price);
	}
	
	public void applyDiscount(Discount discount) {
		this.discountStrategy = discount;
	}
}
{% endhighlight %} 

What about case when there is no discount?<br/>
Simply add discount, where we return full price:<br/>

{% highlight java %}
public class NoDiscount implements Discount {
	
	public BigDecimal compute(BigDecimal price) {
		return price;
	}
}
{% endhighlight %} 

So finally, our Product class should look like that:<br/>

{% highlight java %}
public class Product {
	
	private String name;
	private BigDecimal price;
	private Discount discountStrategy;

	public Product(String name, BigDecimal price) {
		this.name = name;
		this.price = price;
		this.discountStrategy = new NoDiscount();
	}
	
	public BigDecimal computePrice() {
		return discountStrategy.compute(price);
	}
	
	public void applyDiscount(Discount discount) {
		this.discountStrategy = discount;
	}
}
{% endhighlight %} 

Now we can use our classes in practice. <br/>
Now we can create class called Order, where we'll store all Products and summarise price<br/>
and also we can create our Main class to make it work.<br/>

{% highlight java %}
public class Order {
	private ArrayList<Product> products = new ArrayList<Product>();

	private String summarise() {
		BigDecimal summarisedPrice = new BigDecimal("0");
		for(Product : products) {
			summarisedPrice = BigDecimal.add(product.computePrice());
		}
	}
	public void addProduct(Product product) {
		products.add(product);
	}
	public void removeProduct(Product product) {
		if(products.contains(product) {
			product.remove(product);
		}
	}
}
{% endhighlight %} 

And in Main class we can do this:<br/>

{% highlight java %}
public class Main {
	
	public static main(String[] args) {
		Product p1 = new Product("Drink Mix", 5);
		Product p2 = new Product("Snacks Nice", 5);
		Product p3 = new Product("Water COOL", 5);
		
		p1.applyDiscount(new NewClientDiscount());
		p2.applyDiscount(new StudentDiscount());
		
		Order o = new Order();
		o.addProduct(p1);
		o.addProduct(p2);
		o.addProduct(p3);
		
		System.out.println("Summarised price is " + o.summarisedPrice();
		);
	}
}
{% endhighlight %} 

So that's how you can implement strategy pattern. It's quite easy to implement it.<br/>
Let's see on good sides and bad sides of this pattern.<br/>
So good thing is that you can create class which doesn't have to be touched every time<br/>
when you want to implement new algorithm to compute your discount. And you don't have write 
those if's statements.<br/>

From the other side, you have to know what algorithm you want to implement and you have to<br/>
create new class for each discount algorithm.<br/>
Ok, and that's all you have to know to use stategy pattern in your project.<br/>
Have fun!<br/>