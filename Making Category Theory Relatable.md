# Introduction

Matrices are one of the first tools you meet in university math. They let you package together systems of linear equations, which can then be solved algorithmically with Gaussian elimination. This is a natural generalisation of the school-level treatment of simultaneous equations; you can implement addition and multiplication of equations as row operations on the corresponding matrix, reducing it to row echelon form.

There's a trick which relates these operations to standard matrix multiplication. Any row operation on some matrix $A$ can be implemented by just multiplying on the left with a fixed matrix $M$ - and the way you find $M$ is just by applying the operation to the identity matrix!

For example, we can take $\begin{pmatrix} 1 & 2 \\ 5 & 7 \end{pmatrix}$, and implement the operation of subtracting $5$ times the first row from the second row, to leave us with $\begin{pmatrix} 1 & 2 \\ 0 & -3 \end{pmatrix}$. Simply apply the same operation to the identity matrix, so $\begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}$ goes to $\begin{pmatrix} 1 & 0 \\ -5 & 1 \end{pmatrix}$, and one can verify that $\begin{pmatrix} 1 & 0 \\ -5 & 1 \end{pmatrix} \begin{pmatrix} 1 & 2 \\ 5 & 7 \end{pmatrix} = \begin{pmatrix} 1 & 2 \\ 0 & -3 \end{pmatrix}$.

So, when we solve a linear system $A \vec x = \vec b$ using row operations, we can view it as multiplying on the left by a series of matrices, $R_1, R_2, \dots$, until we reduce the system to something more tractable.

That's all well and good, but _why_ does the trick work? Why should "following the identity" matrix give us all the information about the row operation? And what on earth does this have to do with Category Theory?

As it turns out, the answer lies in focusing not on what the identity matrix "is", but what it "does", how it relates to other matrices. And to do this, we will take a detour into studying two of the fundamental concepts of Category Theory - _covariance_ and _contravariance_.
# Covariance

Let's go back to basics - and I mean, the _real_ basics. Addition and multiplication!

We often take for granted the commutative property of addition. $2 + 9$ is the same as $9 + 2$, since they both give the same result, $11$. But to a small child, the former is actually a lot harder! You have to start at $2$, and then count up by $9$, whereas it's much easier to start at $9$ and count up by $2$. Even if the _result_ is the same, the _operations performed_ are quite different - so, knowing about commutativity gives you the freedom to choose the more convenient route.

But there's another perspective on numbers which makes the commutative property a lot more obvious - as sizes of finite sets. Say you have 2 cherries and 3 bananas. You can combine them into a single collection of 5 fruits by taking their "union", and then count how many there are, giving their size.

Or, you can take their sizes individually, and then... add the numbers together!

![[Yoneda Talk Image 4.png|400]]

Our "size" function here relates inputs to outputs, as all functions do. But moreover, it's _relational_ - given a way to relate the inputs, "union", there's a corresponding way to relate the outputs, "addition"! And this is what allows us to see commutativity of addition - "union" is obviously commutative as an operation on collections (up to bijection), and we can transport this commutativity along the "size" function.

We can make a similar observation with multiplication. $2 \times 9$ gives the same _result_ as $9 \times 2$, but is distinct _operationally_. The former requires you to add together 9 copies of "2", whereas the latter requires you to add together 2 copies of "9". Commutativity gives you the freedom to choose which route to take.

And again, it's easy to deduce this property by viewing numbers as sizes of finite sets. We can take the cartesian product and make a grid of all possible choices, and then count them up, or we can take the sizes individually, and then multiply the numbers together! Commutativity simply follows from transporting the commutativity of "product" along the "size" function.

![[Yoneda Talk Image 5.png|500]]

These examples illustrate the concept of _covariance_. We consider functions that not only map inputs to outputs, but map _relations between inputs_ to _relations between outputs_ - which let's us transport ideas in one domain to ideas in another. It's a good notion of "translation between perspectives".

And that's great, because different perspectives are useful for different purposes! It's not exactly practical to carry out a large multiplication by drawing out an entire grid, after all - there are fast algorithms developed for numbers we can use instead. What matters is not having any One True Perspective, but instead having multiple, so long as we have this ability to _translate between them_.
# Contravariance

After you get comfortable with arithmetic, you might try using numbers to describe real-world phenomena. Other than "size", another common way numbers get used is as _measurements_.

Say you're measuring a stick. Given a unit of measurement, you get back a numerical value - say, centimetres gives 50. And given a different one, you get a different value - metres gives 0.5. There's a way to relate these inputs - a metre is 100 centimetres. And the way to relate the outputs "goes backwards" - 50 is 100 times 0.5.

![[Yoneda Talk Image 10.png|300]]

Of course, here you can just view it as an example of covariance since the output arrow is reversible. But I think it's useful to emphasise the "inverse" relation on outputs - in fact, the same reasoning is why vector components transform contravariantly. We just consider a function assigning, to each basis, the components of the vector in that basis.

![[Pasted image 20240814214745.png|300]]

Moreover, what's often useful is that covariance and contravariance can combine to give _invariance_. This is why we always write down measurements with both the unit and the number - the unit changes covariantly, the number changes contravariantly, and together they give an invariant notion: "length"! And with vectors, one can "contract" covariant and contravariant indices together.

You also might remember contravariance from school when having to work with graph transformations. Translating a function $y = f(x)$ by, say, $5$ units to the right requires using the equation $y = f(x - 5)$. A diagram can help make this clearer: ![[Pasted image 20240814213339.png|300]]

We see that the $x$-translation by $5$ units acts in the input - so, to make the arrows match up properly, we must apply the _inverse_ transformation first, subtracting $-5$. It's a general principle that functions are covariant in the output (transformations in the $y$ direction), and contravariant in the input (transformations in the $x$ direction).

Now that we've met covariance and contravariance, let's get back to matrices!

# Matrices

It turns out it'll be a little easier to consider _column_ operations first - we'll then transpose our result to get the version for row operation.

So, a column operation takes in a matrix $A$, and outputs another matrix $C(A)$, such that each column of $C(A)$ is a fixed linear combination of the columns of $A$.

It turns out that column operations are "relational", in the following sense. If there's a way to relate inputs $A$ and $B$, specifically $B = MA$, then there's a way to relate the outputs, so $C(B) = M C(A)$.

![[Yoneda Talk Image 11.png|300]]

This follows fairly quickly from the definition of matrix multiplication - the $j$th column of $MC(A)$ is $M$ applied to the $j$th column of $C(A)$, which is of the form $\sum \lambda_{ij} A_i$ for $A_i$ the $i$th column of $A$. We then just apply linearity to get that $[M C(A)]_j = M \sum \lambda_{ij} A_i = \sum \lambda_{ij} M A_i = [C(MA)]_j = [C(B)]_j$, where the bracket notation denotes the $j$th column.

How does this help us? Well, now that we understand covariance, we're ready to employ a trick - we can write $A = AI$ for $I$ the identity matrix. Then $C(A) = C(A I) = A C(I)$. And that gives our result - the column operation is just right-multiplication by some matrix, and we find it by applying it to the identity matrix!

![[Pasted image 20240815113758.png|300]]

We see that what the identity matrix "does" is relate to every other matrix in a _unique_ way - in category theory, this would be called an "initial object".

How about for row operations? The key insight is that we can implement row operations via "conjugating" a column operation by transpose, as shown:

![[Pasted image 20240815114250.png|300]]

We see that "contravariance" generalises this idea of conjugation. In any case, we have that if $B = AM$, then $R(B) = C(B^T)^T = C((AM)^T)^T = C(M^T A^T)^T = [M^T C(A^T)]^T = R(A) M$. And so $R(A) = R(IA) = R(I) A$, meaning that row operations arise from multiplying on the left by a fixed matrix!

There's a few useful things we immediately get from this result:
- Composing row/column operations can be implemented by multiplying the corresponding matrices.
- By taking determinants, we see that any row/column operation only scales the determinant of the matrix by a constant factor, $\det(R(I))$ or $\det(C(I))$ respectively, when acting on square matrices.
- A row/column operation is invertible if and only if the corresponding matrix is invertible.
- Row and column operations commute with each other! This follows from the associativity of matrix multiplication.

# The Yoneda Lemma


Hopefully, the proof did not feel too difficult. The hard part was more creating useful definitions, covariance and contravariance, that made the problem simple and transparent - which is often what category theory feels like. Indeed, we've seen hints of categorical ideas like initial objects and the Hom functor throughout this piece.

But perhaps most surprisingly, this result is a corollary of one of the first theorems you meet in Category Theory - the Yoneda Lemma. It turns out that this idea of "follow where the identity goes" is the core of the result. The abstract statement of Yoneda simply tells you the most general situation in which this trick works. But, as we saw, it's not necessary to know the abstraction to apply the trick!

Category Theory is normally thought of as very abstract. And indeed, working with generic categories, or understanding the full statement of the Yoneda Lemma, requires a lot of familiarity with abstraction. But this abstraction doesn't necessarily translate to _specific instances_ of categorical theorems or ideas, such as this matrix example.

Indeed, I'm a physicist. I don't really _like_ abstraction - I'm at home performing calculations, working in coordinates, and extracting physical predictions from mathematical models. But I love Category Theory! What I want to show is that Category Theory can be viewed as a bag of techniques and tricks, giving you tools to "think categorically", that can be applied to concrete, tangible problems. Perhaps that's something everyone can appreciate!