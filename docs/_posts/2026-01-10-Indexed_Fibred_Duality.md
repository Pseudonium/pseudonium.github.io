---
layout: post
title: Indexed-Fibred Duality
---

## Comprehending Predicates

Given a set $X$, you can think of a predicate $p(x)$ as an $X$-indexed family of truth values. It outputs "true" or "false" for each element $x \in X$. Indeed, you can view it as a function $$p : X \to \{0, 1\}$$. (More generally, you can think of a function $f : X \to Y$ as an "$X$-indexed family of elements of $Y$").

But there's another equivalent perspective you can take on predicates - indicator functions! Given a predicate $$p : X \to \{0, 1\}$$, you can form the subset $S \subset X$ defined by $$S := \{x \in X \mid p(x) = 1\} = p^{-1}(\{1\})$$. 

This act is called _comprehension_. In the time of naive set theory, it was assumed such an operation was possible for _any_ predicate - given a function that outputs true or false for any $x$, we may form the set of all $x$ for which the function gives "true". Unfortunately, we get contradictory statements from this, the most famous of which is **Russell's paradox**. Taking the predicate $\varphi(x) = (x \not \in x)$, we cannot form a set $$S = \{x \mid x \not \in x\}$$, since $S \not \in S \iff S \in S$. Thus, these days, we restrict comprehension only for predicates defined on already-constructed sets.

While a predicate corresponds to a map _out of_ $X$, a subset corresponds to a map _into_ $X$ - namely, the inclusion map $\iota : S \to X$. Of course, we can go the other way - given a subset $S \subset X$, we can form the indicator function $$\chi_S : X \to \{0, 1\}$$, corresponding to the predicate $\chi_S(x) := (x \in S)$.

Having two equivalent perspectives is quite useful here. For example, I recall being confused about the definition of material implication, $\implies$, particularly why it made sense to let "False implies True" evaluate to "True". However, in subset-world, $\forall x . p(x) \implies q(x)$ corresponds to $$p^{-1}(\{1\}) \subset q^{-1}(\{1\})$$ - just inclusion! This allowed me to transport my intuition from Venn diagrams over to implication; trans women are a subset of all women, so every trans woman is a woman, while there are some women who are not trans women, and some people who are neither. These correspond to "True implies True", "False implies True" and "False implies False" respectively, all of which are consistent with the Venn diagram picture.

Conversely, preimage along a map $f : Y \to X$ in subset-world corresponds to precomposition in predicate-world. More precisely, $$\chi_{f^{-1}(S)} = \chi_S \circ f$$ as functions $$Y \to \{0, 1\}$$. This gives a quick and transparent proof that subset operations - such as intersection, union and complement - necessarily commute with preimage. In predicate-world, these become the logical operations AND,  OR and NOT, which correspond to postcomposition by a map $$\{0, 1\}^k \to \{0, 1\}$$. So preimage preserves these merely because precomposition and postcomposition commute, as a consequence of associativity!

## What are Indexed Families?

In the last section, we observed a correspondence between certain maps _out of_ $X$, predicates $$p : X \to \{0, 1\}$$, and certain maps _into_ $X$, subset inclusions $\iota : S \to X$. As it turns out, we can use this pattern to make sense of "indexed families" more broadly.

For example, sometimes we consider a $J$-indexed family of sets $$(X_j)_{j \in J}$$, for $J$ an index set. If you've studied topology, you'll be familiar with taking arbitrary unions of open sets $$(U_j)_{j \in J}$$, which can be encoded in a function $U_\bullet : J \to \tau$, for $\tau$ the topology on your space.

But in a more general setting, it's not so obvious how to formally define this notion. We can't literally take a function from $J$ to the "set of all sets", since Russell's paradox ensures this is too big to exist. If we know in advance what kinds of sets we'll be dealing with, we can collect them together into a single codomain as in the topological case; but it's unclear how to make this work for _every_ possible $J$-indexed family.

Category theory allows you to cheat and sidestep this issue. From the index set $J$, we can form a _discrete category_ $\text{Disc}(J)$. The objects are elements of $J$, with only identity morphisms. Then, we may view a $J$-indexed family of sets as a functor $X_\bullet : \text{Disc}(J) \to \mathbf{Set}$, sending $j \in J$ to $X_j$, and identity morphisms to identity maps $X_j \to X_j$. Thus, by upgrading $J$ from a plain set to a category, we can view $J$-indexed families of sets as "maps out of $J$", in some generalised sense.

Working by analogy with the previous section, we can investigate whether a similar "comprehension" operation exists, that allows us to view this family as a map _into_ $J$. With a little exploration, you may come up with the following construction: form the "total space" $X = \coprod_{j \in J} X_j$, the disjoint union of all the $X_j$, and then consider the map $p : X \to J$ that sends all of $X_j$ to the index $j$.

In this way, we obtain $$X_j \cong p^{-1}(\{j\})$$. So we've successfully converted a map _out of_ $J$ to a map _into_ $J$, at least up to isomorphism. It's worth noting that we lose information on the intersections between different $X_j$ since they're forced to be disjoint in the total space $X$. Ultimately this is because every $x \in X$ must get mapped to a unique index $p(x) \in J$.

That last remark suggests a strange side-effect of our comprehension operation - we can interpret _any_ map $f : X \to J$ as a $J$-indexed family of sets! Just set $$X_j := f^{-1}(\{j\})$$, sometimes called the _fibre_ over $j \in J$. Thus, the construction we've described gives us a way to translate between $[\text{Disc}(J), \mathbf{Set}]$ and $\mathbf{Set} / J$ - the former is the category of functors $\text{Disc}(J) \to \mathbf{Set}$, while the latter is what's called the _slice category_ over $J$. Its objects are morphisms $X \to J$, and its morphisms are commuting triangles.

In a precise sense, these perspectives are completely equivalent; indeed, we obtain an equivalence of categories $[\text{Disc}(J), \mathbf{Set}] \cong \mathbf{Set} / J$. Much like predicates and subsets, we can either take the "indexed" point of view, via a map _out of_ $J$, or the "fibred" point of view, via a map _into_ $J$.

## Pullbacks as fibre products

Given maps $f : X \to Z$ and $g : Y \to Z$, one can form the _pullback_ $$X \times_Z Y := \{(x, y) \in X \times Y \mid f(x) = g(y)\}$$. This also goes by the name of the "fibre product", and we now have the tools to understand why.

First, we can convert to the "indexed" point of view, by defining $$X_z := f^{-1}(\{z\})$$ and $$Y_z := g^{-1}(\{z\})$$. This allows us to define a new $Z$-indexed family by taking pointwise products, $W_z := X_z \times Y_z$. Returning to the "fibred" point of view, we form $$W := \coprod_{z \in Z} W_z$$ with the projection $p : W \to Z$.

The pullback $X \times_Z Y$ also has a natural projection $\pi : X \times_Z Y$, sending $(x, y) \mapsto f(x)$. One can verify that $$\pi^{-1}(\{z\}) \cong X_z \times Y_z = W_z$$ - in other words, the set $W$ we constructed previously is isomorphic to the pullback! Thus, in indexed terms, the pullback really is just the pointwise product of fibres, hence the name.

## Why Fibred Families?

As we've seen in the preceding sections, there are some operations that make more sense in the "indexed" perspective, and some which make more sense in the "fibred" perspective. It seems that, within mathematics, the fibred point of view is a lot more common, while the indexed point of view is more common in fields like type theory.

One advantage of the fibred approach is that it makes sense in arbitrary categories. Given any category $\mathcal{C}$ and an object $X \in \text{Ob}(\mathcal{C})$, we can form the slice category $\mathcal{C} / X$, and view it as a model for "objects of $\mathcal{C}$ varying over $X$". This works even if there isn't a nice way to directly make sense of $X$-indexed families.

An example that helped me a lot personally was the tangent bundle $TM$ of a smooth manifold $M$. I remember being asked to view the tangent spaces $T_p M$ as a "smoothly varying $M$-indexed family of vector spaces", usually accompanied by a picture of what this might mean intuitively for embedded manifolds. The issue is, it's quite difficult to interpret this statement literally! Not only would I need to make some "class of all vector spaces", I'd also need to give it a smooth structure??

On the other hand, the fibred point of view is significantly more straightforward. We have a smooth map $\pi : TM \to M$ such that $$\pi^{-1}(\{p\}) \cong T_p M$$. The requirement for the family to "vary smoothly" is captured in the smoothness of $\pi$!

In general, it tends to be a lot easier to formalise the fibred point of view, even if what you really want to do are indexed operations. This helps to explain the ubiquity of "fibrations" and related concepts.

## A Glimpse at Moduli

Is it possible to "reverse" the comprehension operation? That is, if we've got an existing concept encoded in the fibred point of view, might we be able to translate it into some kind of indexed point of view? This turns out to be the problem that moduli spaces, or classifying spaces, aim to solve.

We saw previously that you can convert from a subset $S \subset X$ to a predicate $$p : X \to \{0, 1\}$$, going from fibred to indexed. In this case, we can view $$\{0, 1\}$$ as the "moduli space" or "classifying space" for truth values. It lets you realise families of truth values fibred over $X$ as an actual map out of $X$.

For indexed families of sets, one can view $\mathbf{Set}$ as the classifying space for _discrete fibrations_ - families of sets fibred over the objects of some category $\mathcal{C}$.

For the tangent bundle, and vector bundles more generally, the associated classifying space is the **infinite Grassmannian** $\text{Gr}(n, \infty)$. Isomorphism classes of $n$-dimensional bundles over $M$ naturally correspond to homotopy classes of maps $M \to \text{Gr}(n, \infty)$, which lets us convert from the "fibred" point of view to the "indexed" point of view. In a way, one can view $\text{Gr}(n, \infty)$ as providing a solution to the problem of putting a smooth structure on the "class of all vector spaces" (of a fixed dimension).

In general, a moduli/classifying space $S$ is such that maps $M \to S$ allow you to represent fibred families of some type over $M$. Studying the geometry and topology of $S$ can then allow you to deduce _universal_ results about such fibred families. You can also consider which family the identity map $S \to S$ corresponds to - often this takes the form of a "universal" or "generic" such family.

## Further Reading

This post was very much inspired by the early chapters of "Categorical Logic and Type Theory" by Bart Jacobs. Its exposition of fibred and indexed styles was remarkably clear, and it uses the tools of (dependent) type theory to properly explore the indexed point of view. 

I also used the [nlab](https://ncatlab.org/nlab/show/classifying+space) extensively as a reference for fitting together these concepts in my head. I was tempted to add a section on the way in which indexed-fibred duality manifests via interconverting between presheaves on a topological space $X$ and continuous maps $\pi : E \to X$, and how this restricts to an equivalence of categories between sheaves on $X$ and etale maps $p : P \to X$, but perhaps that can be a story for another time...