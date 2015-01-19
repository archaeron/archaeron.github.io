---
layout:     post
title:      Purescript Typeclasses
date:       2014-09-15 11:21:29
summary:    This post lists some of purescripts typeclasses
categories: functional programming purescript typeclass
---

This is a cheat sheet for me

### Semigroup

The `(<>)` operator is for 'concatenation', and must be associative: `(a <> b) <> c = a <> (b <> c)`

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

It's also called `lift`, because it lifts a function into the functor: `a -> b` becomes `f a -> f b`.

Other names:

- Scala: `map`
- Elm: `map` or `(<~)` (was `lift` or `(<~)`)
- Haskell: `fmap`

{% highlight haskell %}

class Functor f where
    (<$>) :: forall a b. (a -> b) -> f a -> f b

{% endhighlight %}

### Apply

Apply works well together with a functor. You use the functor for the first argument and the apply for the rest.

Example: `lift3 f x y z = f <$> x <*> y <*> z`

Other names:

- Haskell: `ap`
- Elm: `(~)`

{% highlight haskell %}

class (Functor f) <= Apply f where
    (<*>) :: forall a b. f (a -> b) -> f a -> f b

{% endhighlight %}

### Applicative

{% highlight haskell %}

class (Apply f) <= Applicative f where
    pure :: forall a. a -> f a

{% endhighlight %}

### Traversable

{% highlight haskell %}
class (Functor t, Foldable t) <= Traversable t where
	traverse :: forall a b f. (Applicative f) => (a -> f b) -> t a -> f (t b)
	sequence :: forall a f. (Applicative f) => t (f a) -> f (t a)

{% endhighlight %}

### Bind

{% highlight haskell %}

class (Apply m) <= Bind m where
	(>>=) :: forall a b. m a -> (a -> m b) -> m b

{% endhighlight %}

### Semigroupoid

{% highlight haskell %}

class Semigroupoid a where
	(<<<) :: forall b c d. a c d -> a b c -> a b d

{% endhighlight %}

### Category

{% highlight haskell %}

class (Semigroupoid a) <= Category a where
	id :: forall t. a t t

{% endhighlight %}

### Monad

{% highlight haskell %}

class (Applicative m, Bind m) <= Monad m where

{% endhighlight %}
