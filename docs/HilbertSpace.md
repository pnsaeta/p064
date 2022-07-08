{:menu LinAl}
{::comment}menu-start{:/comment}

<div class="dropdown">
<label id="hamburger-menu"><img id="hamburger" src="figs/hamburger.png"></label>
<div class="dropdown-content">
<ul>
<li><a href="LinearAlgebra.html">Linear Algebra</a></li>
<li><a href="SquareMatrices.html">Special square matrices</a></li>
<li><a href="GaussJordan.html">Gauss-Jordan elimination</a></li>
<li><a href="HilbertSpace.html">Hilbert spaces</a></li>
<li><a href="Diagonalization.html">Diagonalizing a matrix</a></li>
<li><a href="Eigenvectors.html">Eigenvalues, eigenvectors, and completeness</a></li>
<li><a href="NumericalLinearAlgebra.html">Numerical linear algebra in NumPy</a></li>
</ul>
</div>
</div>

{::comment}menu-end{:/comment}


# Hilbert Space

[Back to the top](LinearAlgebra.md)

A **Hilbert space** is a vector space with an inner product that is used to define a distance function for which it is a complete metric space. That is, the “length” of a vector in the space is given by $$\parallel\vb{v}\parallel = \sqrt{(\vb{v},\vb{v})}$$ and the distance between two vectors is defined by $$\parallel \vb{v-w} \parallel = \sqrt{(\vb{v-w}, \vb{v-w})}$$. ([See here](LinearAlgebra.md#complex-spaces) for the definition of inner product for vector spaces over the field of complex numbers.)

The meaning of a **complete metric space** has to do with with limiting sequences of vectors: if a series of vectors, $$\displaystyle \sum_{k=0}^\infty \vb{v}_k$$ converges absolutely — meaning that $$\displaystyle\sum_{k=0}^\infty \parallel \vb{v}_k \parallel < \infty$$ — then the partial sums converge to an element in the Hilbert space.

What is an example of a Hilbert space. Suppose that $$H$$ is the space of all square-integrable one-dimensional real functions of a real variable. That is, the elements $$f$$ of the space $$H$$ satisfy
\begin{equation}\label{eq:square-integrable}
  \int_{-\infty}^{\infty} [f(x)]^2 \dd{x} < \infty
\end{equation}
These functions must die away sufficiently rapidly as $$|x| \to \infty$$ for the integral to exist, and this property ensures that the inner product of two such functions remains a function in the Hilbert space. This means that linear combinations of these vectors in the space remain square-integrable and form (normalizable) vectors in the space.
