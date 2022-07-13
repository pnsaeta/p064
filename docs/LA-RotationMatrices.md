{:menu LinAl}
{::comment}menu-start{:/comment}

<div class="dropdown">
<label id="hamburger-menu"><img id="hamburger" src="figs/hamburger.png"></label>
<div class="dropdown-content">
<ul>
<li><a href="LA-LinearAlgebra.html">Linear Algebra</a></li>
<li><a href="LA-SquareMatrices.html">Special square matrices</a></li>
<li><a href="LA-GaussJordan.html">Gauss-Jordan elimination</a></li>
<li><a href="LA-HilbertSpace.html">Hilbert spaces</a></li>
<li><a href="LA-Diagonalization.html">Diagonalizing a matrix</a></li>
<li><a href="LA-Eigenvectors.html">Eigenvalues, eigenvectors, and completeness</a></li>
<li><a href="LA-NumericalLinearAlgebra.html">Numerical linear algebra in NumPy</a></li>
</ul>
</div>
</div>

{::comment}menu-end{:/comment}


# Rotation Matrices

The matrix 
\\[
  \mat{R}(\theta) = 
    \begin{pmatrix}
  \cos\theta & -\sin\theta \\\ 
  \sin\theta & \cos\theta
  \end{pmatrix}
\\]
rotates a column vector through angle $$\theta$$ in the counterclockwise direction. You can confirm that $$\mat{R}(\pi/2)$$ rotates $$\vu{x} \to \begin{pmatrix}1 \\\ 0\end{pmatrix}$$ into $$\vu{y} \to \begin{pmatrix} 0 \\\ 1 \end{pmatrix}$$ and $$\vu{y}$$ into $$-\vu{x}$$.

We can generalize readily to 3 dimensions, at least for rotations around one of the basis vectors. For example, 
\\[
    \begin{pmatrix}
    \cos\theta & 0 & \sin\theta \\\ 
    0 & 1 & 0 \\\ 
    -\sin\theta & 0 & \cos\theta
    \end{pmatrix}
\\]
rotates a column vector around the $$y$$ axis. All proper rotations (that don't alter the handedness of the basis vectors) have a determinant of 1. Improper rotations, which do change the handedness of the basis vectors, have determinant $$-1$$.

