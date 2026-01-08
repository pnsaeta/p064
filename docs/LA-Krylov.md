{:menu LA}

* toc
{:toc}

## Krylov Sets

First a preliminary definition: given a square matrix $$\mat{A}$$, its **minimal polynomial** is defined by
\begin{equation}\label{eq:minimal-poly}
  q(\mat{A}) = \alpha_0 \mat{I} + \alpha_1 \mat{A} + \alpha_2 \mat{A}^2 + \cdots + \alpha_l \mat{A}^l = 0
\end{equation}
where $$\alpha_0 \ne 0$$ and $$l$$ is called the minimal degree of $$\mat{A}$$. If the dimension of $$\mat{A}$$ is $$N$$, $$l \le N$$.

How can this relation help us solve the prototypical matrix equation
\begin{equation}\label{eq:mateq}
  \mat{A} \vdot \vb{x} = \vb{b}
\end{equation}
for unknown vector $$\vb{x}$$, but given vector $$\vb{b}$$?

Given $$\vb{b}$$, the **Krylov set** is
\\[
  \qty{ \vb{b}, \mat{A}\vdot\vb{b}, \mat{A}^2\vdot\vb{b}, \ldots, \mat{A}^{l-1} \vdot \vb{b} }
\\]
and I claim that the solution to Eq. (\ref{eq:mateq}) is in $$\mat{A}$$'s Krylov set.

To prove the claim, starting from
\\[
    \alpha_0 \mat{I} + \alpha_1 \mat{A} + \alpha_2 \mat{A}^2 + \cdots + \alpha_l \mat{A}^l = 0
\\]
multiply from the left by $$\mat{A}^{-1}$$ to get
\\[
    \alpha_0 \mat{A}^{-1} + \alpha_1 \mat{I} + \alpha_2 \mat{A} + \cdots + \alpha_l \mat{A}^{l-1} = 0
\\]
and isolate the first term:
\\[
    \mat{A}^{-1} = -\frac{1}{\alpha_0} \sum_{j=0}^{l-1} \alpha_{j+1} \mat{A}^j
\\]
Multiplying on the right by $$\vb{b}$$ completes the demonstration:
\begin{equation}\label{eq:Krylov}
   \boxed{ \vb{x} = \mat{A}^{-1} \vdot\vb{b} = -\frac{1}{\alpha_0} \sum_{j=0}^{l-1} \alpha_{j+1} \mat{A}^j\vdot\vb{b} }
\end{equation}
If $$l \ll \mathrm{dim}(\mat{A})$$ — which is a **big if** — we can use this insight to develop an efficient way to solve Eq. (\ref{eq:mateq}). This approach is generally interesting and useful for very large sparse matrices.

## GMRES algorithm

The **generalized minimum residual** method (GMRES) is a robust means of searching iteratively for an approximate solution to Eq. (\ref{eq:mateq}) for *large* square matrices of rank $$N$$ by minimizing $$\|\mat{A}\vdot\vb{x} - \vb{b} \|$$ for $$\vb{x}$$ in a truncated (and orthogonalized) Krylov subspace of size $$m \le N$$.

1. Set $$\vb{r} \leftarrow \vb{b} - \mat{A}\vdot\vb{x}$$ for a starting guess for an eigenvector $$\vb{x}$$.
2. Normalize: $$\mat{Q}_0 \leftarrow \vb{r} / \|\vb{r}\|$$. That is, $$\mat{Q}_0$$ is the normalized column vector of size $$N$$ from which we will build a "quasi-Krylov" subspace.
3. Let $$e_0 \leftarrow \|\mat{Q}_0\| / \|\vb{b}\|$$, the error in the zeroth-order approximation to $$\vb{x}$$.
4. For $$k = 0, 1, 2, \ldots, m-1$$:
    1. Construct column $$k+1$$ of $$\mat{Q}$$ to be an orthonormal quasi-Krylov vector of the first $$k$$ vectors 
    2. blah
