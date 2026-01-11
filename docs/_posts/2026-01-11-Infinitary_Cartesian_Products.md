---
layout: post
title: Infinitary Cartesian Products
---

## The Axiom of Choice

There are a few equivalent versions of the Axiom of Choice, with Zorn's Lemma and the Well-Ordering Principle being the most popular examples. In my mathematical education, the way it was typically stated was as follows:

> If $$(X_i)_{i \in I}$$ is a family of nonempty sets, then the cartesian product $$\prod_{i \in I} X_i$$ is nonempty.

I remember finding it quite difficult to wrap my head around this - if there's some $x_i \in X_i$ for all $i \in I$, can we not just form the infinite tuple of those elements? Why isn't provable from the other axioms of set theory? What even is an "infinite cartesian product"?

In this short note, the goal is to answer all these questions via an alternative way to think about the axiom of choice, in a way that makes transparent why we care about this property and why it might not hold in settings other than set theory.

## Finitary Cartesian Products

It'll be helpful to first recall the definition of finitary cartesian products. Here, we'll use the Kuratowski notion of ordered pair, defined as $$(a, b) := \{\{a\}, \{a, b\}\}$$. If these elements come from parent sets $A$ and $B$, we notice that $\{a\} \in P(A \cup B)$ and $\{a, b\} \in P(A \cup B)$, so that $(a, b) \in P(P(A \cup B))$, where $P$ denotes the power set.

This allows us to define the cartesian product as $$A \times B = \{x \in P(P(A \cup B)) \mid \exists a \in A, \exists b \in B, x = (a, b)\}$$, where the last part of the definition uses equality of sets.

Once we've got binary cartesian products, we automatically obtain the notions of _relation_ and _function_, as well as the ability to make finitary cartesian products. For example, we could take $(A \times B) \times C$ as a ternary cartesian product. However, at this point we start to obtain multiple non-equal choices - for example, we could just as well have taken $A \times (B \times C)$ as a ternary product. In general, this is not literally equal as a set to $(A \times B) \times C$, but it is at least in bijection with the former set. This problem only exacerbates as we go to larger cartesian products.

One might wonder, then, whether it's possible to produce a "uniform" definition of finitary cartesian product that sidesteps these issues. As it turns out, we can! We start by noticing that the notation $A^n$ for the $n$-fold cartesian product of a set with itself looks suspiciously similar to the $X^Y$ notation for the set of functions from $Y$ to $X$.

Here's the strategy. We consider the $n$-element set $$[n] := \{0, 1, \dots, n - 1\}$$, and define $A^n$ to be $A^{[n]}$, i.e. functions from this set to $A$. Given such a function $a_\bullet : [n] \to A$, we then obtain the elements of the ordered tuple $a_0, a_1, \dots, a_{n - 1}$ simply by evaluating $a_\bullet$ at the corresponding index! Thus, once we have binary products, functions allow us to "bootstrap" all finitary products in a uniform way.

How about for finitary products of many different factors, $A_1, \dots, A_n$? Here we can use a trick from [Indexed-Fibred Duality](https://pseudonium.github.io/2026/01/10/Indexed_Fibred_Duality.html). Instead of having a finite family of sets "indexed" by natural numbers, we construct the total space $A = \coprod_{i=1}^n A_i$, and view this as "fibred" over the indexing set $[n]$, with a projection $\pi : A \to [n]$ sending $A_i$ to the index $i-1$.

Then, to specify an ordered tuple, we want a function $f : [n] \to A$ such that for each $i \in [n]$, $f(i) \in A_{i + 1}$ - or more precisely, in the copy of $A_{i + 1}$ sitting inside $A$. We may express this condition equivalently as $\pi(f(i)) = (i + 1) - 1 = i$, so that $(\pi \circ f)(i) = i \quad \forall i \in [n]$. This is then equivalent to saying $$\pi \circ f = \text{id}_{[n]}$$, meaning that $f$ is a _right inverse_ to our projection map $\pi$. Often these maps are called _sections_ - the analogy is that we're taking a "cross-section" of the total space by picking out an element from each set.

Thus, we can more generally define the cartesian product of a finite family of sets $A_1, \dots, A_n$ by forming the total space $A = \coprod_{i=1}^n A_i$ with its projection $\pi : A \to [n]$ and considering a subset of the functions $f \in A^{[n]}$ - namely, those that satisfy $$\pi \circ f = \text{id}_{[n]}$$. This expresses the cartesian product as a _space of sections_ for a fixed projection map.
## Generalising to Arbitrary Products

The strategy we employed in the last section works more generally! Suppose we have some indexed family of sets $$(X_i)_{i \in I}$$. Then we can form the total space $$X = \coprod_{i \in I} X_i$$ together with the projection $\pi : X \to I$ sending all of $X_i$ to the index $i$. We may then define the cartesian product as a space of sections for this map - the subset of $X^I$ consisting of all maps $f$ such that $$\pi \circ f = \text{id}_I$$. This gives us a uniform definition of cartesian product for any family of sets.

How, then, can we interpret the axiom of choice? In the indexed point of view, we need the assumption that each $X_i$ is nonempty, meaning $\forall i \in I, \exists x_i \in X_i$. In the fibred point of view, this corresponds to the projection map being _surjective_ - for every index $i \in I$, there's some $x \in X$ such that $\pi(x) = i$, meaning $x \in X_i$ (or at least, the copy of $X_i$ inside $X$).

Moreover, we can interpret _any_ surjective map $\pi : X \to I$ as encoding a family of $I$-indexed nonempty sets, for which $X$ is the total space, by setting $$X_i := \pi^{-1}(\{i\})$$. Thus, we arrive at the following equivalent characterisation of the axiom of choice:

> Every surjective map has a right inverse.

What I like about this formulation is that there are lots of contexts where it is obviously _false_, in other fields of math. There are plenty of surjective group homomorphisms, continuous maps, smooth maps and more general "structured" maps that don't have a right inverse! Even if every element in the codomain has a preimage, there might not be a consistent way to choose these to assemble into an actual "structured" right inverse.

This also gives a hint towards why the axiom of choice needs to be asserted, and isn't just a consequence of the other axioms of set theory. Ultimately, it's tied to an assumption about how functions between sets work - that they're sufficiently "unstructured" to allow any map to have a right inverse, provided it is surjective. If we're working in constructive contexts, where our maps might need to be "computable" in some sense, then it stands to reason that functions between sets may be too structured to admit sections!
## Further Reading

The [nlab](https://ncatlab.org/nlab/show/axiom+of+choice) has an excellent reference article on the category-theoretic interpretation of the axiom of choice, including how it gets interpreted in topos theory. Topoi of smooth sets, for example, fail to satisfy the axiom of choice because of how structured the maps are.