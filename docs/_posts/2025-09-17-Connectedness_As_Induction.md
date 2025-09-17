---
layout: post
title: Connectedness as an Induction Principle
---

## Bootstrapping Truth

A lecturer explained the _philosophy_ of mathematical induction to me as:

> If you want to prove a statement holds for some object $x$, you may harmlessly assume it holds for any $y < x$.

He was referring to _strong induction_, which is a strategy for proving predicates on the natural numbers: if you can prove $\forall x \in \mathbb{N} [(\forall y \in \mathbb{N} \text{ such that } y < x, P(y)) \implies P(x)]$, then you've proved $\forall x . P(x)$. Inspecting the statement more carefully, we have:
- $(\forall y < 0, P(y)) \implies P(0)$. But since there _aren't_ any natural numbers strictly less than $0$, proving this implication means we've deduced $P(0)$ from no additional hypotheses; alternatively, $(\forall y < 0, P(y))$ is always true. Regardless, we know that $P(0)$ holds.
- Then we know that $\forall y < 1, P(y)$, since we only need to check $P(0)$. So, $P(1)$ holds.
- Then we know that $\forall y < 2, P(y)$, since we only need to check $P(0) \text{ and } P(1)$. So, $P(2)$ holds.

And so on! We've managed to _bootstrap_ the truth of $P(n)$ purely from knowledge of its truth for smaller statements.

You may have already noticed the analogy with ordinary "chain of falling dominoes" induction: if you can prove the base case of $P(0)$, and the inductive step of $\forall k . P(k) \implies P(k + 1)$, then you've proven $\forall x . P(x)$. Again, the truth of $P(0)$ implies that of $P(1)$, and then $P(1)$ being true means $P(2)$ is true, and so on and so forth. Indeed if we apply ordinary induction to the statement $Q(x) := \forall y \in \mathbb{N} \text{ such that } y < x, P(y)$ we recover strong induction.

## Induction Just Got Real

### The Definition

In part this article was inspired by [this stackexchange post](https://math.stackexchange.com/questions/4202/induction-on-real-numbers?noredirect=1&lq=1), which talks about a generalisation of induction for the real numbers. It's a _hybrid_ of strong and regular induction that applies for intervals of the form $[a, b]$ and $[a, \infty)$. Suppose you have some subset $S \subseteq [a, b]$ or $S \subseteq [a, \infty)$ that we view as the subset on which some predicate $p(x)$ holds, such that:
- $a \in S$, which acts as our "base case".
- If $x \in S$ then there's some $\epsilon > 0$ such that $[x, x + \epsilon) \subset S$, which acts as our "ordinary inductive step".
- If $[a, y) \subset S$ then $y \in S$, which acts as our "strong inductive step".

Then we can deduce that $S$ is the _entirety_ of our interval! I like to view this as _marching_ from $a$ rightwards (for concreteness take $a = 0$):
- We know that $0 \in S$.
- Then there's some $\epsilon_0 > 0$, maybe $0.1$, such that $[0, 0.1) \subset S$ by ordinary induction. In fact by strong induction we have $[0, 0.1] \subset S$.
- Since $0.1 \in S$ there's an $\epsilon_1 > 0$, maybe $0.01$, such that $[0.1, 0.11] \subset S$ (combining both kinds of induction).
- Continuing, perhaps we get $[0.11, 0.111] \subset S$, and then $[0.111, 0.1111] \subset S$, and so on and so on...
- We seem to be getting stuck at $0.1111 \dots = \frac 19$. But using strong induction, we'd have $[0, \frac 19) \subset S$, so $\frac 19 \in S$, and we can resume our march!

Every time we've reached some point $\alpha$, we can always march a little positive distance further. And even if we run into a [Zeno's paradox](https://en.wikipedia.org/wiki/Zeno%27s_paradoxes) situation where we appear to be converging to some finite upper bound, we can use the strong inductive step to finish the whole process and continue our march.

### The Proof

Of course, we should justify _why_ the principle of "real induction" works. Consider what a "minimal counterexample" could be:
- Suppose for contradiction that $S$ is _not_ the whole interval $I$. We consider the set of "counterexamples" $$C = \{y \in I \mid y \not \in S\}$$, the complement of $S$.
- By the first step $C$ is nonempty. It's also bounded below by $a$, since it's a subset of our interval $I = [a, b]$ (or $I = [a, \infty)$).
- So it has an infimum $\inf C$, which is our analog of the "minimal counterexample".
- Suppose it actually _is_ a counterexample, so $\inf C \not \in S$. Then we necessarily have $[a, \inf C) \subset S$ since $\inf C$ is a lower bound for the set of counterexamples. But by strong induction we deduce $\inf C \in S$, a contradiction!
- So it must not be a counterexample, meaning $\inf C \in S$. But then by ordinary induction there's some $\epsilon > 0$ where $[\inf C, \inf C + \epsilon) \subset S$. This contradicts $\inf C$ being the _greatest_ lower bound of the set of counterexamples, since e.g. $\inf C + \frac 12 \epsilon$ also works.
- So $S$ must really be the whole interval!



### The Intermediate Value Theorem

The linked stackexchange post gives a few different examples of proving statements in analysis with "real induction". One of my favourites is the intermediate value theorem! I like to use this strategy:
- Take $f : [a, b] \to \mathbb{R}$, where $f(a) > 0$ and $f(b) < 0$. Suppose, for contradiction, that $f$ is never $0$.
- Let $$S = \{x \in [a, b] \mid f(x) > 0\}$$. Our goal will be to use real induction to show that $S = [a, b]$, which is a contradiction since $f(b) < 0 \implies b \not \in S$.
- We've already established the base case of $a \in S$, since $f(a) > 0$.
- For regular induction, take an $x \in S$ where $f(x) > 0$. Since $f$ is continuous there's a region around $x$ where $f$ is positive, so some $\epsilon > 0$ where $\forall y \in [x, x + \epsilon)$, $f(y) > 0$. This means $[x, x + \epsilon) \subset S$ and thus regular induction holds.
- For strong induction suppose $[a, y) \subset S$, so $\forall a \leq t < y, f(t) > 0$. Then by continuity, $f(y) \geq 0$. But we've already assumed $f$ is never zero - so we must have $f(y) > 0$ and thus $y \in S$. Therefore strong induction holds!
- So $S = [a, b]$ which we've already shown is a contradiction. Thus $f$ must be zero somewhere.


## Diffusive Induction

Can we generalise the style of the previous argument to other "continuous" settings? One immediate issue is the lack of an _order_ in general metric or topological spaces - going by the philosophy of induction, we need some kind of way to say when one point "comes before" another. But as the MSE post explains, there's a way to generalise induction to a disordered situation via _connectedness_!

Let $X$ be a connected topological space, meaning you cannot write it as the union of two nonempty disjoint open subsets. Suppose $S \subseteq X$ satisfies the following properties:
- $S$ is nonempty, so there's some $x_0 \in S$. This is our "base case".
- $S$ is open, so whenever $x \in S$, there's some open set $U$ such that $x \in U \subseteq S$. This is our "ordinary induction".
- $S$ is closed, so whenever $A \subseteq S$, we have $\bar A \subseteq S$. This is our "strong induction".

Then $S = X$! Because otherwise, if $S^c$ was nonempty, then $X = S \cup S^c$ partitions $X$ into two nonempty disjoint open subsets (note that $S^c$ is open since $S$ is closed).

Similar to the "marching" analogy from before, I like to view this form of topological induction as a kind of _diffusion_ process. We have a source of water at $x_0 \in S$, which spreads throughout our space - both via "ordinary induction" using openness, and via "strong induction" using closedness. So long as our space is connected, water eventually covers it all!

This _is_ a generalisation since real induction is a form of topological induction:
- The base case of $S$ being nonempty is the same in both cases.
- $S$ being open corresponds to $(x - \epsilon, x + \epsilon) \subset S$ for some $\epsilon > 0$ whenever $x \in S$, meaning $[x, x + \epsilon) \subset S$.
- $S$ being closed corresponds to $[a, y) \subset S \implies y \in S$.

## Looking Ahead

Here's a list of directions you can go in:
- There are ways to frame applications of connectedness as a kind of "induction" proof - that a connected locally path connected space is path-connected, or that a continuous image of a connected space is connected.
- Another equivalent formulation of connectedness is "chain connectedness", which states that if $X$ is connected and $\bigcup_{i \in I} U_i = X$ is an open cover, then any two points $x, y \in X$ are connected by a finite "chain" $x \in U_{i_0}, U_{i_0} \cap U_{i_1} \neq \emptyset, \dots, U_{i_{n - 1} } \cap U_{i_n} \neq \emptyset, y \in U_{i_n}$ of open sets from the cover. This is better suited to using connectedness as a "local to global" translation, where you can deduce something holds everywhere by showing it holds _locally_ and that you can patch sets on which it holds together.
- It's also possible to view compactness as a similar kind of "induction principle" - see [this post](https://www.drmaciver.com/2015/03/topological-compactness-is-an-induction-principle/) for more details.
- The style of "real induction" also generalises nicely to _transfinite induction_ over ordinals, where the "ordinary induction" step becomes proving truth for successor ordinals, and the "strong induction" step becomes proving truth for limit ordinals.
- This arxiv paper goes into significantly more detail on the applications of real induction - https://arxiv.org/pdf/1208.0973.pdf.
- You may have noticed I did a little bait-and-switch by equating "induction on predicates" with "induction on subsets". Strictly speaking, the former is _first-order induction_ while the latter is _second-order induction_ and is stronger.
- Sometimes induction doesn't even respect the usual order! Cauchy's proof of the AM-GM inequality uses a kind of "forward-backward induction" where he establishes its truth for all powers of $2$, and then works backwards from there.

If I were to adapt my lecturer's quote to encompass these more general formulations of induction, I might try:
> If you want to prove $P(x)$, don't consider it in isolation. Consider how $x$ _relates_ to other objects $y$, and whether you can leverage the truth of $P(y)$ to deduce $P(x)$.

Indeed, if $x$ ranges over an infinite set $X$, you _can't_ just provide a separate proof of $P(x)$ for every $x \in X$. There isn't enough ink in the universe to write all of that down! We need some kind of _uniformity_ or _pattern_ in the reason that $P(x)$ is true, and/or a way to _relate_ $P(x)$ and $P(y)$ to each other if $x$ and $y$ are related in some way. Of course, this focus on "relationships between objects" is a cornerstone of category theory :)