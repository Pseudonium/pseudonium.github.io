# Making Category Theory Relatable

#[SoMEpi](https://some.3b1b.co/)

Matrices are one of the first tools you meet in university math. They let you package together systems of linear equations, which can then be solved algorithmically with Gaussian elimination. This is a natural generalisation of the school-level treatment of simultaneous equations; you can implement addition and multiplication of equations as row operations on the corresponding matrix, reducing it to row echelon form.

There's a trick which relates these operations to standard matrix multiplication. Any row operation on some matrix $A$ can be implemented by just multiplying on the left with a fixed matrix $M$ - and the way you find $M$ is just by applying the operation to the identity matrix!

For example, we can take $\begin{pmatrix} 1 & 2 \\\\ 5 & 7 \end{pmatrix}$, and implement the operation of subtracting $5$ times the first row from the second row, to leave us with $\begin{pmatrix} 1 & 2 \\\\ 0 & -3 \end{pmatrix}$. Simply apply the same operation to the identity matrix, so $\begin{pmatrix} 1 & 0 \\\\ 0 & 1 \end{pmatrix}$ goes to $\begin{pmatrix} 1 & 0 \\\\ -5 & 1 \end{pmatrix}$, and one can verify that $\begin{pmatrix} 1 & 0 \\\\ -5 & 1 \end{pmatrix} \begin{pmatrix} 1 & 2 \\\\ 5 & 7 \end{pmatrix} = \begin{pmatrix} 1 & 2 \\\\ 0 & -3 \end{pmatrix}$.

So, when we solve a linear system $A \vec x = \vec b$ using row operations, we can view it as multiplying on the left by a series of matrices, $R_1, R_2, \dots$, until we reduce the system to something more tractable.

That's all well and good, but _why_ does the trick work? Why should "following the identity" matrix give us all the information about the row operation? And what on earth does this have to do with category theory?

As it turns out, the answer lies in focusing not on what the identity matrix "is", but what it "does", how it relates to other matrices. And to do this, we will take a detour into studying two of the fundamental concepts of category theory - _covariance_ and _contravariance_.
## Covariance

Let's go back to basics - and I mean, the _real_ basics. Addition and multiplication!

We often take for granted the commutative property of addition. $2 + 9$ is the same as $9 + 2$, since they both give the same result, $11$. But to a small child, the former is actually a lot harder! You have to start at $2$, and then count up by $9$, whereas it's much easier to start at $9$ and count up by $2$. Even if the _result_ is the same, the _operations performed_ are quite different - so, knowing about commutativity gives you the freedom to choose the more convenient route.

But there's another perspective on numbers which makes the commutative property a lot more obvious - as sizes of finite sets. Say you have 2 cherries and 3 bananas. You can combine them into a single collection of 5 fruits by taking their "union", and then count how many there are, giving their size.

Or, you can take their sizes individually, and then... add the numbers together!

![Addition diagram](https://github.com/user-attachments/assets/cc314079-f1cf-4b41-8447-286d2505ff8e)


Our "size" function here relates inputs to outputs, as all functions do. But moreover, it's _relational_ - given a way to relate the inputs, "union", there's a corresponding way to relate the outputs, "addition"! And this is what allows us to see commutativity of addition - "union" is obviously commutative as an operation on collections (up to bijection), and we can transport this commutativity along the "size" function.


Starting with
![Addition Commutativity](https://github.com/user-attachments/assets/fe90ae7b-8531-40d8-88ff-52650e0aeb99)
we can obtain
![Addition Numerical Commutativity](https://github.com/user-attachments/assets/b3f856a2-dbcf-48d4-9cd0-6a59e2366435)

We can make a similar observation with multiplication. $2 \times 9$ gives the same _result_ as $9 \times 2$, but is distinct _operationally_. The former requires you to add together 9 copies of "2", whereas the latter requires you to add together 2 copies of "9". Commutativity gives you the freedom to choose which route to take.

And again, it's easy to deduce this property by viewing numbers as sizes of finite sets. We can take the cartesian product and make a grid of all possible choices, and then count them up, or we can take the sizes individually, and then multiply the numbers together! Commutativity simply follows from transporting the commutativity of "product" along the "size" function.

![Multiplication Diagram](https://github.com/user-attachments/assets/223a4cd3-4e95-4985-9858-9a3be7d0ba9c)


These examples illustrate the concept of _covariance_. We consider functions that not only map inputs to outputs, but map _relations between inputs_ to _relations between outputs_ - which lets us transport ideas in one domain to ideas in another. It's a good notion of "translation between perspectives". I like to think of the naming as saying that as the inputs vary, the outputs "co-vary" alongisde them, in a consistent way.

And that's great, because different perspectives are useful for different purposes! It's not exactly practical to carry out a large multiplication by drawing out an entire grid, after all - there are fast algorithms developed for numbers we can use instead. What matters is not having any One True Perspective, but instead having multiple, so long as we have this ability to _translate between them_.
## Contravariance

After you get comfortable with arithmetic, you might try using numbers to describe real-world phenomena. Other than "size", another common way numbers get used is as _measurements_.

Say you're measuring a stick. Given a unit of measurement, you get back a numerical value - say, centimetres gives 50. And given a different one, you get a different value - metres gives 0.5. There's a way to relate these inputs - a metre is 100 centimetres. And the way to relate the outputs "goes backwards" - 50 is 100 times 0.5.

![Measurement Diagram](https://github.com/user-attachments/assets/37e3d783-1348-43d5-a021-3c774718f233)


Of course, here you can just view it as an example of covariance since the output arrow is reversible. But I think it's useful to emphasise the "inverse" relation on outputs - in fact, the same reasoning is why vector components transform contravariantly. We just consider a function assigning, to each basis, the components of the vector in that basis.

![image](https://github.com/user-attachments/assets/3bfd3ac5-1178-4325-8033-fa00a06e5135)


Moreover, what's often useful is that covariance and contravariance can combine to give _invariance_. This is why we always write down measurements with both the unit and the number - the unit changes covariantly, the number changes contravariantly, and together they give an invariant notion: "length"! With vectors, specifying both the basis and the components gives the invariant notion of "arrow in space".

You also might remember contravariance from school when having to work with graph transformations. Translating a function $y = f(x)$ by, say, $5$ units to the right requires using the equation $y = f(x - 5)$. A diagram can help make this clearer: ![image](https://github.com/user-attachments/assets/297547f8-27e8-46af-b485-50e8cef8faa5)


We see that the $x$-translation by $5$ units acts in the input - so, to make the arrows match up properly, we must apply the _inverse_ transformation first, subtracting $-5$. It's a general principle that functions are covariant in the output (transformations in the $y$ direction), and contravariant in the input (transformations in the $x$ direction).

So, contravariance is pretty similar to covariance - it's still the case that relations between inputs get mapped to relations between outputs. But there's a kind of "flipping" involved, similar to multiplying by $-1$ - as the inputs vary, the outputs "contra-vary" in a consistent way, hence the name. In fact, if we take our relations between inputs to be $\leq$, this is quite literally true:

![image](https://github.com/user-attachments/assets/d2749b53-9c47-456a-b9b2-5fad16afcd88)

I.e. if $a \leq b$, then $-b \leq -a$.

Now that we've met covariance and contravariance, let's get back to matrices!

## Matrices

### Column Operations

It turns out it'll be a little easier to consider _column_ operations first - we'll then transpose our result to get the version for row operation.

So, a column operation takes in a matrix $A$, and outputs another matrix $C(A)$, such that each column of $C(A)$ is a linear combination of the columns of $A$. This linear combination is allowed to vary from column to column - for example, perhaps we swap the first two columns and leave all others unchanged. But it's not allowed to depend explicitly on $A$ itself.

It turns out that column operations are "relational", in the following sense. If there's a way to relate inputs $A$ and $B$, specifically $B = MA$, then there's a way to relate the outputs, so $C(B) = M C(A)$.

![image](https://github.com/user-attachments/assets/8ec0c479-bd6e-4a97-9f10-029f0af7fe79)

All we need to prove this are the definitions of column operations and matrix multiplication! Focusing on the first column, we have that $$[C(A)]_1 = \lambda_{11} [A]_1 + \lambda_{12} [A]_2 + \dots + \lambda_{1n} [A]_n$$, where the bracket notation denotes the operation of taking the $j$th column. If we were swapping the first two columns, then we'd have $\lambda_{12} = 1$ and $\lambda_{1j} = 0$ otherwise, $\lambda_{21} = 1$ and $\lambda_{22} = 0$ otherwise. This just expresses the idea that the column operation consists of applying a linear combination to the columns of $A$.

The point is that this operation of "taking the $j$th column" interacts very nicely with matrix multiplication! We can express this in the following diagram:

![image](https://github.com/user-attachments/assets/76ff5a64-deba-4c02-80bf-5f5c6a7d0914)

Indeed, matrix multiplication is _defined_ so that this diagram "commutes" - both ways of getting from the bottom-left corner to the top-right corner give the same _result_, even though the _operations performed_ are different. This lets us deduce that $$[MC(A)]_1 = M [C(A)]_1 = M (\lambda_{11} [A]_1 + \lambda_{12} [A]_2 + \dots + \lambda_{1n} [A]_n)$$.

But matrices, by definition, act linearly! So, we can distribute $M$ across the linear combination, and obtain:

$$M (\lambda_{11} [A]_1 + \lambda_{12} [A]_2 + \dots + \lambda_{1n} [A]_n) = \lambda_{11} M [A]_1 + \dots + \lambda_{1n} M [A]_n$$

And finally, by the definition of matrix multiplication, we can "pass M through the brackets", to finally get:

$$\lambda_{11} M [A]_1 + \dots + \lambda_{1n} M [A]_n = \lambda_{11} [MA]_1 + \dots + \lambda_{1n} [MA]_n = [C(MA)]_1 = [C(B)]_1$$, where we recall that $B = MA$.

Extending this logic to all the other columns, we've successfully proven that $C(B) = C(MA) = M C(A)$!

How does this help us? Well, now that we understand covariance, we're ready to employ a trick - we can write $X = XI$ for $I$ the identity matrix of the appropriate size, and $X$ our starting matrix. Then, using $M = X$ and $A = I$, we get $C(X) = C(X I) = X C(I)$. And that gives our result - the column operation is just right-multiplication by some matrix, and we find it by applying it to the identity matrix!

![image](https://github.com/user-attachments/assets/f901c9f7-80d3-43ea-8df5-59b82d3f433e)

We see that what the identity matrix "does" is relate to every other matrix in a _unique_ way - in category theory, this would be called an "initial object". And that's what lets us describe the entire column operation by a single matrix - the result of the column operation on the identity matrix.

This also explains why column operations are "relational". If we have $B = MA$, then $C(B) = B C(I) = (MA) C(I) = M (A C(I)) = M C(A)$, using the associativity of matrix multiplication!

### Row Operations

How about for row operations? These take in a matrix $A$ and produce a matrix $R(A)$, such that each _row_ of $R(A)$ is a linear combination of the rows of $A$, where again this linear combination cannot depend on $A$ but can vary from row to row. The definition of matrix multiplication won't particularly help us here, unfortunately - but there's still hope!

The key insight is that we can implement row operations via "conjugating" a column operation by transpose, as shown:

![image](https://github.com/user-attachments/assets/0db1cc99-f664-44d1-a02c-d2c9597ee0d5)

In other words, we can apply the row operation by first swapping rows and columns, then applying a related column operation (using the same linear combinations as the row operation), and then transposing again. We see that "contravariance" generalises this idea of conjugation, and gives us the formula $R(A) = C(A^T)^T$.

In any case, we have that if $B = AM$, then $R(B) = C(B^T)^T = C((AM)^T)^T = C(M^T A^T)^T = [M^T C(A^T)]^T = R(A) M$. And so $R(X) = R(IX) = R(I) X$, meaning that row operations arise from multiplying on the left by a fixed matrix!

There's a few useful things we immediately get from this result:
- Composing row/column operations can be implemented by multiplying the corresponding matrices.
- By taking determinants, we see that any row/column operation only scales the determinant of the matrix by a constant factor, $\det(R(I))$ or $\det(C(I))$ respectively, when acting on square matrices.
- A row/column operation is invertible if and only if the corresponding matrix is invertible.
- Row and column operations commute with each other! Applying a row operation to $X$ means multiplying on the left by some $M$, and applying a column operation means multiplying on the right by some $N$. But $(MX)N = M(XN)$, since matrix multiplication is associative.

## The Yoneda Lemma


Hopefully, the proof did not feel too difficult. The hard part was more creating useful definitions, covariance and contravariance, that made the problem simple and transparent - which is often what category theory feels like. Indeed, we've seen hints of categorical ideas like initial objects, commutative diagrams and the Hom bifunctor throughout this piece.

But perhaps most surprisingly, this result is a corollary of one of the first theorems you meet in category theory - the Yoneda Lemma. Informally, it tells you that there's an equivalence between what an object "is" and what it "does", how it relates to other things, and how to use it. And as we saw, applying that idea to the identity matrix let us deduce the entire form of the row/column operation.

It turns out that this idea of "follow where the identity goes" is the core of the result, even when you get to the formal proof of the lemma. The abstract statement of Yoneda simply tells you the most general situation in which this trick works. But, as we saw, it's not necessary to know the abstraction to apply the trick!

Category theory is normally thought of as very abstract. And indeed, working with generic categories, or understanding the full statement of the Yoneda Lemma, requires a lot of familiarity with abstraction. But this abstraction doesn't necessarily translate to _specific instances_ of categorical theorems or ideas, such as this matrix example.

Indeed, I'm a physicist. I don't really _like_ abstraction - I'm at home performing calculations, working in coordinates, and extracting physical predictions from mathematical models. But I love category theory! What I want to show is that category theory can be viewed as a bag of techniques and tricks, giving you tools to "think categorically", that can be applied to concrete, tangible problems. Perhaps that's something everyone can appreciate!

[Discuss this article on Reddit](https://www.reddit.com/r/math/comments/1et3y2d/making_category_theory_relatable/).

Emily Riehl has a [talk](https://www.youtube.com/watch?v=SsgEvrDFJsM) where she approaches this from a much more categorical lens. If you want to get into category theory more broadly, I'd recommend Leinster's _Basic Category Theory_, and Bartosz Milewski's _Category Theory for Programmers_ (his YouTube series is excellent too).

I'm planning to continue writing articles explaining Mathematics and Physics. If you'd like to support me, consider [buying me a coffee](https://ko-fi.com/pseudonium).
