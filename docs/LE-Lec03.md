{:menu LE}

# Lecture 3 — Linear Independence and Matrix Inverses
* toc
{:toc}

## Question

Are the following three vectors in $$\mathbb{R}^3$$ linearly independent?
\begin{equation}
    (1, 2, 3) \qquad (-3, -2, -1) \qquad (2, 3, 4)
\end{equation}
That is, can you write one of them as a linear combination of the other two?

## Problem — Gram-Schmidt Orthogonalization

Given a set of linearly independent vectors that are not necessarily orthogonal, Gram-Schmidt orthogonalization is a procedure to generate an orthonormal set of basis vectors from the given set. The strategy is straightforward:

1. Normalize the first vector $$\vb{a}_1$$ by dividing by its magnitude to get $$\vb{e}_1$$.
2. Form a vector orthgonal to $$\vb{e}_1$$ by subtracting from $$\vb{a}_2$$ its projection along $$\vb{e}_1$$:
\begin{equation*}
  \vb{a}'_2 = \vb{a}_2 - (\vb{a}_2 \cdot \vb{e}_1) \vb{e}_1
\end{equation*}
3. Normalize $$\vb{a}'_2$$ to produce $$\vb{e}_2$$.

Given the three vectors
\begin{equation}
    (1, 2, 3) \qquad (-3, -2, -1) \qquad (2, 3, 2)
\end{equation}
form an orthonormal set of basis vectors in which $$\vb{e}_1$$ is parallel to $$(1, 2, 3)$$.