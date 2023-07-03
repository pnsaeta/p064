{:menu LA}
{::comment}menu-start{:/comment}

<div class="dropdown">
<label id="main-menu"><img id="master" src="figs/master.webp"></label>
<div class="dropdown-content">
<ul>
<li><a href="SW-Installation.html">Software Installation</a></li>
<li><a href="LA-LinearAlgebra.html">Linear Algebra</a></li>
<li><a href="FO-Intro.html">Fourier Series and Transforms</a></li>
<li><a href="ST-Random.html">Stochastic Processes</a></li>
<li><a href="DE-DE1.html">Differential Equations</a></li>
<li><a href="PD-PD1.html">Partial Differential Equations</a></li>
<li><a href="PR-Project.html">Projects</a></li>
</ul>
</div>
</div>
<div class="dropdown hamburger">
<label id="hamburger-menu"><img id="hamburger" src="figs/hamburger.webp"></label>
<div class="dropdown-content">
<ul>
<li><a href="LA-LinearAlgebra.html">Linear Algebra</a></li>
<li><a href="LA-SquareMatrices.html">Square Matrices</a></li>
<li><a href="LA-GaussJordan.html">Gauss-Jordan Elimination</a></li>
<li><a href="LA-HilbertSpace.html">Hilbert Space</a></li>
<li><a href="LA-Diagonalization.html">Diagonalization</a></li>
<li><a href="LA-Eigenvectors.html">Eigenvalues and Eigenvectors of Square Matrices</a></li>
<li><a href="LA-NumericalLinearAlgebra.html">Numerical Linear Algebra with NumPy</a></li>
<li><a href="LA-Krylov.html">Krylov Sets</a></li>
<li><a href="LA-NumericalLinearAlgebra.html">Numerical Linear Algebra with NumPy</a></li>
</ul>
</div>
</div>

{::comment}menu-end{:/comment}


# Hilbert Space

[Back to the top](LA-LinearAlgebra.md)

A **Hilbert space** is a vector space with an inner product that is used to define a distance function for which it is a complete metric space. That is, the “length” of a vector in the space is given by $$\parallel\vb{v}\parallel = \sqrt{(\vb{v},\vb{v})}$$ and the distance between two vectors is defined by $$\parallel \vb{v-w} \parallel = \sqrt{(\vb{v-w}, \vb{v-w})}$$. ([See here](LA-LinearAlgebra.md#complex-spaces) for the definition of inner product for vector spaces over the field of complex numbers.)

The meaning of a **complete metric space** has to do with with limiting sequences of vectors: if a series of vectors, $$\displaystyle \sum_{k=0}^\infty \vb{v}_k$$ converges absolutely — meaning that $$\displaystyle\sum_{k=0}^\infty \parallel \vb{v}_k \parallel < \infty$$ — then the partial sums converge to an element in the Hilbert space.

What is an example of a Hilbert space? Suppose that $$H$$ is the space of all square-integrable one-dimensional real functions of a real variable. That is, the elements $$f$$ of the space $$H$$ satisfy
\begin{equation}\label{eq:square-integrable}
  \int_{-\infty}^{\infty} [f(x)]^2 \dd{x} < \infty
\end{equation}
These functions must die away sufficiently rapidly as $$|x| \to \infty$$ for the integral to exist, and this property ensures that the inner product of two such functions remains a function in the Hilbert space. This means that linear combinations of these vectors in the space remain square-integrable and form (normalizable) vectors in the space.
