---
layout:     post
title:      The Expressiveness Of Types
date:       2014-10-07 11:21:29
summary:    One of the reasons why I love functional programming
categories: functional programming types why-i-love-fp
---

Let's assume we have a function `drawWeather` that displays weather information on the screen.

{% highlight java %}
drawWeather(Sky.SUNNY, 10, 30, 4);
{% endhighlight %}

When you see a function like this in java, how do you tell what the different arguments do?
What happens if I switch the arguments by mistake?


Compare the java version to the FSharp version. Every argument is clear and the compiler will tell you if you switched arguments, because now we have specific types for the different units and not just `int`s.

{% highlight fsharp %}
drawWeather Sunny 10<percent> 30<celsius> 4<kmh>
{% endhighlight %}

or even

{% highlight fsharp %}
drawWeather Sunny (Humidity 10<percent>) (Temp 30<celsius>) (Wind 4<kmh>)
{% endhighlight %}

It is possible to make the types more expressive in Java, but the language makes it a lot harder.

In F# you need this for the wind velocity:

{% highlight fsharp %}
[<Measure>] type kmh
type Wind = Wind of int<kmh>
{% endhighlight %}

Or in Haskell:

{% highlight fsharp %}
drawWeather Sunny (Humidity 10) (Temp 30) (Wind 4)
{% endhighlight %}
