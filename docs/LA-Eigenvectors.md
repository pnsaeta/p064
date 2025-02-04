{:menu LA}

* toc
{:toc}


## Eigenvalues and Eigenvectors of Square Matrices

Consider the matrix
\\[
    \mat{A} = \begin{pmatrix}
      1 & 1 & 1 \\\ 1 & 1 & 1 \\\ 1 & 1 & 1
    \end{pmatrix}
\\]
which consists of three copies of the same column vector. Clearly, the rows of this matrix are *not* linearly independent; if we were to attempt to reduce $$\mat{A}$$ to $$\mat{U}$$ form, we would get
\\[
    \mat{U} =  \begin{pmatrix}
      1 & 1 & 1 \\\ 0 & 0 & 0 \\\ 0 & 0 & 0
    \end{pmatrix}
\\]
Only the first column has a pivot; the second and third columns do not. The matrix has **rank** 1 (the number of nonzero pivots) and the **nullspace** has dimension $$n-r=2$$. In solving $$\mat{U}\vdot\vb{x} = 0$$, we have two free variables, corresponding to the free columns (2 and 3). The nullspace satisfies
\\[
    \begin{pmatrix}
      1 & 1 & 1 \\\ 0 & 0 & 0 \\\ 0 & 0 & 0
    \end{pmatrix} \vdot
    \begin{pmatrix}
    x \\\ y \\\ z
    \end{pmatrix} = 0
\\]
which requires that 
\begin{equation}\label{eq:constraint}
    x = -(y + z)
\end{equation}
This is the equation of a plane; $$y$$ and $$z$$ are arbitrary, but once they are specified, there is a unique value of $$x$$. We can construct a basis for the nullspace by letting each of the free variables ($$y$$ and $$z$$) be zero and forming the vector consistent with Eq. (\ref{eq:constraint}). Hence, the vectors $$\begin{pmatrix} -1 & 1 & 0 \end{pmatrix}^{\rm T}$$ and $$\begin{pmatrix} -1 & 0 & 1\end{pmatrix}^{\rm T}$$ constitute a basis for the nullspace.

What are the eigenvalues and eigenvectors of $$\mat{A}$$? That is, for what values of $$\vb{x}$$ and $$\lambda$$ is
\\[
    \mat{A} \vdot \vb{x} = \lambda \vb{x} = \lambda \mat{I} \vdot \vb{x}
    \qqtext{or}
    (\mat{A} - \lambda\mat{I})\vdot\vb{x} = 0
\\]
For a nontrivial value of $$\vb{x}$$ to satisfy this equation, the matrix $$\mat{A} - \lambda\mat{I}$$ must be singular; its determinant must vanish:
\\[
    \mathrm{det} \begin{pmatrix} 1 - \lambda & 1 & 1 \\\ 1 & 1 - \lambda & 1 \\\ 1 & 1 & 1 - \lambda \end{pmatrix} = 0
\\]
Expanding in minors gives
\begin{align}
    (1-\lambda)[(1-\lambda)^2 - 1] + 1 [1 - (1-\lambda)] + 1 [1 - (1-\lambda)] &= 0 \notag \\\ 
    (1-\lambda)(-2\lambda + \lambda^2) + 2 \lambda &= 0 \notag \\\ 
    \lambda \qty[(1-\lambda)(\lambda-2)+2] &= 0 \notag \\\ 
    \lambda \qty[-\lambda^2 +3\lambda -2 + 2] &= 0 \notag \\\ 
    \lambda^2 (3 - \lambda)  &= 0 \notag
\end{align}
Two eigenvalues are 0, and a third is 3. What are the corresponding eigenvectors? I'll start with $$\lambda = 3$$ and substitute into $$\mat{A} - \lambda\mat{I}$$ to get
\\[
    \begin{pmatrix}
      -2 & 1 & 1 \\\ 1 & -2 & 1 \\\ 1 & 1 & -2
    \end{pmatrix} \vdot \begin{pmatrix}
    x \\\ y \\\ z
    \end{pmatrix} = 0
\\]
which is clearly satisfied by $$x=y=z$$ or 
\\[
    \vb{x}\_{1} = \begin{pmatrix}
    1 \\\ 1 \\\ 1
    \end{pmatrix}
\\]

What about for $$\lambda = 0$$? If we successively choose $$y = 0$$ and $$z = 0$$, then we get the two eigenvectors
\\[
  \vb{x}\_2 = \begin{pmatrix} 1 \\\ 0 \\\ -1 \end{pmatrix}  
  \qqtext{and}
  \vb{x}\_3 = \begin{pmatrix} 1 \\\ -1 \\\ 0 \end{pmatrix}  
\\]

## Gram-Schmidt Orthogonalization

While $$\vb{x}_2$$ and $$\vb{x}_3$$ are orthogonal to $$\vb{x}_1$$, they are not orthogonal to each other. Often it is most convenient to construct an orthonormal set of eigenvectors. Normalizing the first two gives
\\[
    \vb{e}\_1 = \begin{pmatrix}
      \frac{1}{\sqrt{3}} \\\ \frac{1}{\sqrt{3}} \\\ \frac{1}{\sqrt{3}}
    \end{pmatrix}
    \qqtext{and}
    \vb{e}\_2 = \begin{pmatrix}
    \frac{1}{\sqrt{2}} \\\ 0 \\\ -\frac{1}{\sqrt{2}}
    \end{pmatrix}
\\]
where I am using $$\vb{e}_i$$ for the normalized (basis) eigenvectors.
We can construct a vector from $$\vb{x}_3$$ that is orthogonal to $$\vb{x}_2$$ by subtracting from $$\vb{x}_3$$ its projection onto (normalized) $$\vb{e}_2$$:
\\[
    \vb{x}'\_3 = \vb{x}\_3 - (\vb{x}\_3 \vdot \vb{e}\_2) \vb{e}\_2
    = \begin{pmatrix}
    1 \\\ -1 \\\ 0
    \end{pmatrix} - \frac{1}{\sqrt{2}} \begin{pmatrix}
    \frac{1}{\sqrt{2}} \\\ 0 \\\ -\frac{1}{\sqrt{2}}
    \end{pmatrix}
    = \begin{pmatrix}
    \frac12 \\\ -1 \\\ \frac12
    \end{pmatrix}
\\]
You can readily confirm that $$\vb{x}'_3$$ is orthogonal to both $$\vb{x}_1$$ and $$\vb{x}_2$$, but it is not yet normalized. Dividing by $$\sqrt{\vb{x}'_3 \vdot \vb{x}'_3}$$ yields the complete set of orthonormal eigenvectors:
\\[
    \vb{e}\_1 = \begin{pmatrix}
      \frac{1}{\sqrt{3}} \\\ \frac{1}{\sqrt{3}} \\\ \frac{1}{\sqrt{3}}
    \end{pmatrix}
    \qqtext{and}
    \vb{e}\_2 = \begin{pmatrix}
    \frac{1}{\sqrt{2}} \\\ 0 \\\ -\frac{1}{\sqrt{2}}
    \end{pmatrix}
    \qqtext{and}
    \vb{e}\_3 = \begin{pmatrix}
    \frac{1}{\sqrt{6}} \\\ -\frac{2}{\sqrt{6}} \\\ \frac{1}{\sqrt{6}}
    \end{pmatrix}
\\]
In summary, **Gram-Schmidt orthogonalization** of a set of linearly independent but nonorthogonal vectors $$\vb{x}_j$$ to yield an orthonormal set of basis vectors $$\vb{e}_j$$ consists first in selecting an initial vector and normalizing it:
\\[
    \vb{e}\_1 = \frac{\vb{x}\_1}{\sqrt{\vb{x}\_1 \vdot \vb{x}\_1}}
\\]
and then for each subsequent vector, projecting out all previous normalized vectors before normalizing the result:
\\[
    \vb{x}'\_i = \vb{x}\_i - \sum\_{j=1}^{i-1} (\vb{x}\_i \vdot \vb{e}\_j)\vb{e}\_j
\\]
and then normalizing
\\[
    \vb{e}\_i = \frac{\vb{x}'\_i}{\sqrt{\vb{x}'\_i \vdot \vb{x}'\_i}}
\\]

While Gram-Schmidt orthogonalization is mathematically sound, the good folks who wrote *Numerical Recipes* point out that “because of the build-up of roundoff errors, naïve Gram-Schmidt orthogonalization is *terrible*. (Emphasis in the original.) They go on to explain that the right way to build an orthonormal basis for a subspace is by [singular value decomposition](LA-NumericalLinearAlgebra.md#singular-value-decomposition) (SVD).