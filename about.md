---
layout: page
title: About monkey2
permalink: /about/
---

Monkey2 is a new programming language currently under development designed for creating cross-platform apps and games.

Monkey2 features a clean, clear syntax that is largely self-documenting. For example, here is how you declare a class in monkey2:

{% highlight monkey %}
Class MyClass Extends BaseClass

   Field x:Float
   Field y:Float
   Field vx:Float
   Field vy:Float

   Method Update()
	Print( "Updating!" )
	x+=vx
	y+=vy
   End
End
{% endhighlight %}

However, despite its simple syntax, monkey2 also provides support for a wide range of modern programming techniques, including:

* Automatic memory management
* Generic classes and functions
* Stack allocated structs
* Operator overloading
* First class functions
* Anonymous 'lambda' functions
