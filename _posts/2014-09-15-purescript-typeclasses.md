---
layout:     post
title:      Purescript Typeclasses
date:       2014-09-15 11:21:29
summary:    This post lists some of purescripts typeclasses
categories: functional programming purescript typeclass
---

This is a cheat sheet for me

### Semigroup

The `(<>)` operator is for concatenation, and must be associative: `(a <> b) <> c = a <> (b <> c)`

{% highlight haskell %}

class Semigroup a where
    (<>) :: forall a.a -> a -> a

{% endhighlight %}

### Monoid
A monoid describes how to accumulate a result with the type `m`

{% highlight haskell %}

class (Semigroup m) <= Monoid m where
    mempty :: m

{% endhighlight %}

### Functor

A functor has a `map` function `(<$>)`.
Other names i've found:

    -   Scala: `map`
    -   Elm: `lift`
    -   Haskell: `fmap`


{% highlight haskell %}

class Functor f where
    (<$>) :: forall a b. (a -> b) -> f a -> f b

{% endhighlight %}

### Apply

Apply works well together with a functor. You use the functor for the first argument and the apply for the rest.
Example: `lift3 f x y z = f <$> x <*> y <*> z`

{% highlight haskell %}

class (Functor f) <= Apply f where
    (<*>) :: forall a b. f (a -> b) -> f a -> f b

{% endhighlight %}

### Applicative

{% hightlight haskell %}

class (Apply f) <= Applicative f where
    pure :: forall a. a -> f a

{% endhightlight %}