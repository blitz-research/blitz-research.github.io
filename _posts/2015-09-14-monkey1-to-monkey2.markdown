---
layout: post
title: "Converting monkey1 code to monkey2"
data: 2015-09-14 10:17:00
categories: monkey2 update
---

A quick list of things to consider when converting monkey1 code to monkey2...

# Strict mode not an option!

All functions that return something must return something! In monkey1, you could omit return statements even in functions that returned non-void. Not so in monkey2 (although this isn't actually implemented in the compiler yet..).

Variables no longer default to int - all variable declarations must either specify a type, or be initialized with a value, eg:

{% highlight monkey %}
Local blah			'Wont work in monkey2!
Local blah:Int			'Ok in monkey1 and monkey2.
Local blah:=10			'Ok in monkey1 and monkey2 - blah is int.
Local blah:Int=10		'Ok in monkey1 and monkey2
{% endhighlight %}

Method and function declarations can still omit a return type, however the default return type in monkey2 is void (as opposed to int in monkey1).

The monkey1 shortcut type specifiers (eg: % for int and # for float) are not supported in monkey2  - you must use ':Int', ':Float' etc.


# Using namespaces and importing files

_Note: This section highly subject to change._

In monkey2, there is no need to import modules as all modules are now automagically imported for you.

However, it is still necessary to know what 'namespaces' the various declarations (ie: function, classes etc) you want to use are located in.

The easiest way to deal with this for now is to add this to the top of your source files:

{% highlight monkey %}
Using std
Using mojo
Using mojo2
{% endhighlight %}

This will allow you to access ALL decalarations in the std and mojo namespaces.

To import monkey2 source files into a build, use the preprocessor #Import directive, eg:

{% highlight c %}
#Import "file2.monkey2"
{% endhighlight %}


# Function call parameters must be enclosed in parenthesis

In monkey1, you could (usually...) omit the paranthesis around function parameters, eg: 

{% highlight monkey %} 
DrawImage image,x,y	'will not work in monkey2!
{% endhighlight %}

In monkey2, this is not allowed - all function parameters must be enclosed in parenthesis, eg:

{% highlight monkey %}
DrawImage( image,x,y )	'works in monkey1 and monkey2
{% endhighlight %}


# Array initializers must use New

Monkey1 allowed a 'quick' form of array initializer:

{% highlight monkey %}
Local tmp:Int[10]	'wont work in monkey2!
{% endhighlight %}

In monkey2, you need to use the longer (but equivalent) form:

{% highlight monkey %}
Local tmp:=New Int[10]	'works in monkey1 and monkey2!
{% endhighlight %}


# Virtual and overriding methods must be explicitly marked

_Note: This section highly subject to change._

In monkey1, all non-final methods are automatically virtual and can (sometimes inadvertantly) dynamically override existing methods. In monkey2, virtual and overriding methods must be marked as such, eg:

{% highlight monkey %}
Class Base
	Method Update() Virtual
	End
End

Class Derived Extends Base
	Method Update() Override
	End
End
{% endhighlight %}


# Property syntax changes

Code that declares properties will need to use the new syntax. Instead of this...

{% highlight monkey %}
Method MyProp:String() Property	'monkey1 only!
{% endhighlight %}

...you will to need to use...

{% highlight monkey %}
Property MyProp:String()	'monkey2 only!
{% endhighlight %}


# End-of-line handling

_Note: Subject to change..._

Monkey2 uses similar end-of-line handling to monkey1, but is stricter.

All 'block' declarations (Class, Method, Property, Function) and block statements (If, While, Repeat, Select) must be of the following form:

_header_<br>
..._content_...<br>
_footer_<br>

_header_ and _footer_ must start on a new line, and be the only thing on that line. Declarations can no longer be 'mashed up' onto a single line. For example:

{% highlight monkey %}
Class MyClass Extends BaseClass	'class declaration header
	Method Update()		'method declaration header
	End			'method declaration footer
End				'class declaration footer
{% endhighlight %}

Multiple statements can appear on a single line, as long as they are separated by the statement separator token ';', eg:

{% highlight monkey %}
For Local i:=0 Until 100
	Print( i );Print( i*2 );Print( i*3)
Next
{% endhighlight %}

Finally, monkey2 ignores any end-of-line tokens that appear after any of the following: '(', '[' and ','. This allows you to split function parameter lists and auto array elements over mulitple lines.


# No fancy slices (yet?).

Instead of this...

{% highlight monkey %}
Local x:=t[x..]			'monkey1 only!
Local y:=t[..y]
Local z:=t[x..y]
{% endhighlight %}

...use this...

{% highlight monkey %}
Local x:=t.Slice( x )		'monkey2 only!
Local y:=t.Slice( 0,y )
Local z:=t.Slice( x,y )
{% endhighlight %}

