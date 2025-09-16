---
layout: post
title: Three Perspectives on Equivalence Relations
---

## What is Abstraction?

There's a quote by the mathematician Henri Poincaré:
> Mathematics is the art of giving the same name to different things.

It speaks to the prevalence of identifying and studying _patterns_ - seemingly different objects share enough common properties that it makes sense to talk about them all simultaneously. It doesn't matter if you have 2 apples and 3 oranges, or 2 buses and 3 cars, or 2 planets and 3 beavers; in each case, the total amount of things is 5. So we can view the statement "$2 + 3 = 5$" as the "name" given to the common idea underlying all these scenarios!

This is a prototype of the way abstraction is handled within mathematics - we focus on the shared _properties_ of otherwise different things. And as it turns out, there's a rather convenient way to formalise it!

## A Literal Interpretation

Let's take Poincaré's quote and interpret it as straightforwardly as possible. We have a collection of "things" that we'll call $X$, and we have some "naming" function $f : X \to N$, where $N$ is our collection of names. Then the idea is that it's possible to have $$f(x) = f(y)$$ but $$x \neq y$$ - i.e. we've given the same name to different things, quite literally!

What we've done is provide a "coarser" version of equality, where we consider elements with the same name to be related, even if they aren't literally equal. Formally, we could define a relation by: $$x \sim y \text{ whenever } f(x) = f(y)$$. This has a name within category theory - it's called the **kernel pair** associated to our function $f$. Notice that:
- Our relation is reflexive - since we always have $f(x) = f(x)$, we always have $x \sim x$
- Our relation is symmetric - since $f(x) = f(y) \implies f(y) = f(x)$, we always have $x \sim y \implies y \sim x$
- Our relation is transitive - if $f(x) =  f(y)$ and $f(y) = f(z)$, then $f(x) = f(z)$ by transitivity of equality. Unfolding definitions, we obtain $x \sim y \text{ and } y \sim z \implies x \sim z$


In other words... we've obtained an equivalence relation! Indeed, many equivalence relations you've met before arise as a kernel pair - if you take $f$ to be "remainder modulo $12$", you obtain the equivalence relation on the integers used in "clock arithmetic". So you might wonder - do _all_ equivalence relations arise this way?

## Equivalence Relations as Abstraction

Let's try and work backwards. Suppose we start with a set $X$, and have an equivalence relation $\sim$ on it. Can we find some set $Y$ and a function $f : X \to Y$ such that $x \sim y \iff f(x) = f(y)$?

For this, it'll be useful to consider the other common perspective on equivalence relations - **partitions**. Any $x_0 \in X$ defines an equivalence class $$[x_0] = \{ x \in X \mid x_0 \sim x \}$$, and these classes partition our set $X$ up into disjoint "regions".

What we can do, then, is form the **quotient set**, the "set of equivalence classes", $$X / \sim  \space := \{[x] \mid x \in X\}$$, as a set of sets. Moreover, this comes equipped with a standard map from $X$ called the **quotient map**, $q : X \to X / \sim$, sending $x \mapsto [x]$.

That's about as much information as we can get in general from an equivalence relation; and, fortunately for us, it turns out to be sufficient! Note that:
- If $x \sim y$, then the equivalence class for $x$ is the same as that for $y$, so $[x] = [y]$
- Conversely, if $[x] = [y]$, then $y \in [y]$ by reflexivity, so $y \in [x]$, so $x \sim y$.

In other words, our equivalence relation is the kernel pair of the quotient map! We can view $q$ as a "naming" function, where the "name" associated to elements of $X$ is their equivalence class - usually a rather long-winded name, of course...

## Looking Ahead

So we've seen that there are 3 perspectives one can take on equivalence relations:
- The standard definition, as a reflexive, symmetric, transitive relation
- As partitions, in terms of chopping up the set into disjoint pieces
- As kernel pairs, in terms of relating elements that share the same _properties_, encoded by a function $f : X \to Y$

It turns out the last perspective generalises quite well to more complicated situations like groups and rings - the kernel pair associated to a group homomorphism $f : G \to H$ is an equivalence relation that automatically respects the group structure! In the sense that if $x \sim y$ and $z \sim w$ then $xz \sim yw$. Moreover, the equivalence class of the identity is always a normal subgroup.

In general, for "algebraic" structures, we see that $f(x) = f(y) \iff f(x - y) = 0 \iff x - y \in \ker f$ for the usual notion of "kernel", so it provides an essentially equivalent formulation that makes sense for "non-algebraic structures" like sets. This also illustrates how statements like "injective iff trivial kernel" arise. :)