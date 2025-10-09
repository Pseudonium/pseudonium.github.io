---
layout: post
title: A Precise Notion of Approximation
---

## Heaps of trouble

Take a sizeable heap of sand (metaphorical or, if you're near a beach, physical!). There are too many grains to count manually but I think it's reasonable to assume that at least 1 million are present. A pile is massive compared to a single grain; so much so that adding or removing 1 grain should leave it looking basically indistinguishable.

But hang on - if a million grains is a heap, and removing 1 grain leaves it a heap, then 999999 grains should be a heap too. And then 999998 grains should be a heap as well. 999997, then 999996, then 999995... continuing inductively, we arrive at the conclusion that a single grain of sand is a heap, and then that _zero_ grains of sand form a heap! Meaning that we should constantly be surrounded by an uncountably infinite number of heaps of sand, everywhere, all the time - a heap of trouble, indeed.

This is the _Sorites paradox_, otherwise known as the _paradox of the heap_. It illustrates the difficulty of trying to give a precise definition to something like "a pile of sand" in terms of a numerical threshold. The notion is inherently "fuzzy", meaning we expect small changes to a pile of sand should leave it a pile. And yet, enough small changes can add up to a big change!

A similar issue arises if you want to try and rigorously define $\approx$ - what it means for two numbers to be "close" to each other, such that they're "approximately equal":
- Suppose we say $1 \approx 1.00000000000001$.
- Then it seems reasonable to say that $1.00000000000001 \approx 1.00000000000002$, so we get $1 \approx 1.00000000000002$
- Continuing inductively, we get $1 \approx 2$
- After longer, we might get $1 \approx 1000$
- With significant effort, we obtain $1 \approx 10^{10^{100} }$, at which point "approximately equal to" has lost all meaning.

Just like the sorites paradox, it's the desired transitivity that bites us. We can't produce a sensible notion of $\approx$ that lets us chain statements together, so that $a \approx b \text{ and } b \approx c \implies a \approx c$.

But if you've taken a class in calculus, you'll likely have come across the idea of "approximation" in some way:
- Continuity at $a$ means that inputs near $a$ get mapped to outputs near $f(a)$, which you could write as $x \approx a \implies f(x) \approx f(a)$.
- Differentiability means that, when you zoom in, the function "looks like" a straight line, which allows you to approximate values of $f$ near $a$ using the derivative. Again, we could write this as $x \approx a \implies f(x) \approx f(a) + f'(a) (x - a)$.
- Integrability is all about trying to approximate the area under the graph of $f$ by a Riemann sum of thin rectangles.

As it turns out, there's a loophole in the argument I gave above which lets us sidestep the Sorites paradox, and make sense of these instances of $\approx$ _rigorously_! But first, we'll need to delve into the duality of _hard_ vs _soft_ analysis...

## Quantitative vs Qualitative


Notice that the sense of approximation we were looking for initially was _qualitative_ - either $1 \approx 2$ or $1 \not \approx 2$. The question had a yes/no answer, and we saw that ultimately it wasn't possible to define $\approx$ this way without falling victim to the Sorites paradox.

However, it's straightforward to give a _quantitative_ notion of approximation, by saying _how_ close two numbers are. Indeed, the real numbers come equipped with a natural notion of "distance", where the distance between $x$ and $y$ is $\mid x - y\mid$.

So, we could say that $1$ and $1.01$ are "within $0.1$ of each other", or "$0.1$-close", since $\mid 1 - 1.01 \mid \leq 0.1$. Similarly, $\pi$ is $0.2$-close to $3$, which is then $0.3$-close to $e$. Of course, we could refine precisely how close $3$ and $\pi$ are by computing more digits of the decimal expansion, just like how we could say $1$ and $1.01$ are also $0.03$-close to each other.

Chaining these together can be a little tricky. For example, while $1$ is $0.01$-close to $1.01$, which is $0.01$-close to $1.02$, it is not true that $1$ is $0.01$-close to $1.02$. This is what the triangle inequality is meant to deal with - if $a$ is $0.01$-close to $b$ and $b$ is $0.01$-close to $c$, then we can only guarantee $a$ is $0.01 + 0.01 =0.02$-close to $c$. Combining $\approx$ statements necessarily leads to a lost of "approximation strength", which is behaviour that a simple yes/no question can't exhibit.

This suggests that approximation should fundamentally be thought of as a _quantitative_ concept. We can't say "$x$ is close to $a$", but we _can_ say "$x$ is $\delta$-close to $a$" by supplying a tolerance $\delta$ that specifies the _strength_ of our approximation. Our quantitative perspective lies at the heart of _hard analysis_, which deals with precise numerical estimates and bounds on quantities. The standard $\epsilon$-$\delta$ definition fits quite neatly into this framework - you give me a tolerance on the output, and I can provide you a tolerance on the input.

Still, it would be rather convenient to have a "soft" analog of analysis. In this world, we could freely make more "qualitative" statements that didn't depend on specific tolerances, but nonetheless still retained a level of mathematical rigor. Here, we really could define $\approx$ to have a yes/no answer, and reason more _logically_ than _numerically_. Perhaps I could even say "for small $x$, $\sin(x) \approx x$" in a way that made sense mathematically...

Such a world, perhaps surprisingly, does exist! But to reach it, we'll need to figure out a way to sidestep the Sorites paradox. It forbids us from saying $a \approx b$ for two numbers $a$ and $b$, after all.

In fact, it prevents more than that. We can run a quite similar argument to show that "closeness" doesn't make _qualitative_ sense for pairs of numbers - or, points in a plane. If $\vec a \approx \vec b$, then we should be able to make a little translation and say $\vec b \approx \vec c$, where $\vec c - \vec b = \vec b - \vec a$. Continuing inductively, we'd deduce that $\vec a$ is "close" to points $\vec x$ arbitrarily far from it, perhaps billions of light years away, at which point "closeness" has once again lost all meaning.

Indeed, in any finite number of dimensions, we can always run a Sorites-type argument. So vectors, as points in $\mathbb{R}^n$, cannot support a qualitative notion of approximation. If we're to have any hope of escaping the paradox, there's only one option... go to infinite dimensions!

## Escaping the Paradox, eventually

We can interpret "infinite dimensions" as corresponding to _sequences_ of real numbers, $a_\bullet : \mathbb{N} \to \mathbb{R}$ denoting $a_0, a_1, a_2, a_3, \dots$. One key difference between these and finite lists is that sequences allow you to talk about _eventual_ behaviour. I can have a sequence $(a_n) = 4, 10, 3, -4, 6, 0, 0, 0, 0, \dots$, and another that goes $(b_n) = -100, 2312123, 12398123, -223982323, 1234123124, ..., 129389123, 0, 0, 0, 0, \dots$.

These differ at the start, but _eventually_ end up doing the same thing, staying constant at $0$. (Sometimes I like to imagine the sequences partying and going wild in their youth, before getting sucked into the system and conforming as they age...). While $a_n = 0$ isn't _always_ true, it's still eventually true.

In fact, the infinite size of $\mathbb{N}$ lets you define a notion of "eventual truth" that has no finite analog! We say that a predicate $p(n)$ is _eventually true_ if, at some point $N$, $p$ holds true for all $n \geq N$. For example:
- The sequences given in the first paragraph have $a_n = 0$ and $b_n = 0$ being eventually true.
- Eventually, we have that $n^2 > 10000n + 9999$
- For any polynomial $p(n)$, it's eventually true that $2^n > p(n)$.
- For any positive number $\epsilon$, it's eventually true that $\frac 1n < \epsilon$.

There are also plenty of statements that do _not_ hold eventually:
- $n$ is even
- $n$ is a perfect square
- $n$ is not a perfect square
- $n$ is prime
- $n$ is composite (trickier, follows from the proof of there being infinitely many primes!).

If we tried to copy this definition to a finite set like $\{0, 1, 2, 3, 4\}$, then a predicate $p(n)$ being "eventually true" would just reduce to $p(4)$ being true. It's the fact that $\mathbb{N}$ doesn't explicitly contain $\infty$, and yet still contains "arbitrarily large" numbers, that allows it to support a nontrivial notion of eventual truth!

Let's go back to the quantitative notion of approximation we already know: two numbers $a$ and $b$ are $0.1$-close if $\mid a - b \mid \leq 0.1$. What should the analog for sequences $(a_n)$ and $(b_n)$ be? Well, the natural quantity to consider would be $\mid a_n - b_n \mid \leq 0.1$ - but since this is a predicate on $\mathbb{N}$, we can ask for this to only hold _eventually_, rather than for all $n$!

So, we can make sense of two sequences being eventually $0.1$-close, and eventually $0.01$-close, and eventually $0.001$-close... in fact, for any positive real number $\epsilon$, it makes sense to ask whether or not two sequences are eventually $\epsilon$-close.

This lets us _finally_ define a "qualitative" notion of approximation that has just a yes/no answer, rather than being dependent on a specific approximation strength. We say that $(a_n) \approx (b_n)$ if they are _arbitrarily_ close, eventually. Namely, for any $\epsilon > 0$, $\mid a_n - b_n \mid < \epsilon$ eventually!

With that, the paradox really does get sidestepped; there's no finite distance between $(a_n)$ and $(b_n)$ that we can chain to get "close" sequences differing by billions of light years, but it still allows us to say that _different_ sequences, like $(\frac 1n)$ and $(- \frac 1n)$, are nonetheless "close".

## Looking Ahead

I really do view it as almost miraculous that "soft", qualitative analysis is possible, given the strength of the Sorites paradox. But it turns out $\infty$ is precisely what we needed to circumvent it, by allowing us to establish a _new notion of truth_ - one where a predicate $p(n)$ doesn't need to hold for all $n$, just for "sufficiently large" $n$!

It turns out this generalises quite nicely to all other notions of "limit" in analysis, through the concepts of _directed sets_, _nets_ and _filters_. These can all be viewed as ways to formalise this intuition of "eventually" or "sufficiently X" values:
- We could say a predicate $p$ on the real numbers holds "eventually" if, at some point $x_0$, we have $p(x)$ true for all $x \geq x_0$.
- We could also alter the direction, and have $p(x)$ true for all $x \leq x_0$ at some point, to model predicates that hold "eventually" as $x$ gets increasingly negative.
- We could also direct ourselves towards a particular point $a$, and say that it holds "near" $a$ if, at some $x_0$, $\mid x - a \mid \leq \mid x_0 - a \mid \implies p(x)$. But much like the finite set case, we need to exclude $a$ itself for this to not collapse to just the truth of $p(a)$.

There's also a dual concept to "eventual truth", which you could call "frequent truth". You might've spotted earlier that, if $p(n)$ does _not_ hold eventually, then $\neg p(n)$ must hold "infinitely often". Formally, we might say that a predicate $q(n)$ holds "frequently" if, no matter how large a $N$ we choose, there's some $n \geq N$ such that $q(n)$ holds. If $q(n)$ does _not_ hold frequently, then it must occur only finitely many times - meaning that $\neg q(n)$ holds eventually, establishing the duality! This comes up when trying to show limits don't exist, for example.

I would recommend looking at [Limits: A New Approach to Real Analysis](https://link.springer.com/book/10.1007/978-1-4612-0697-2) for further exposition on this perspective. Terence Tao's blogpost on the [Finite convergence principle](https://terrytao.wordpress.com/2007/05/23/soft-analysis-hard-analysis-and-the-finite-convergence-principle/) also heavily inspired the ideas used in this article. I've found thinking in terms of "qualitative" vs "quantitative" analysis, and how infinity supports new kinds of "truth", to be quite an interesting and fruitful perspective on analysis :)