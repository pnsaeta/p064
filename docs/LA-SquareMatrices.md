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



# Square Matrices

Square matrices have a number of interesting properties and deserve special attention.

* toc
{:toc}

## Identity Matrix

The identity matrix has ones along the main diagonal and zeros everywhere else:
\begin{equation}
  \mat{I} = \begin{pmatrix}
    1 & 0 & 0 & \cdots & 0 \\\ 
    0 & 1 & 0 & \cdots & 0 \\\ 
    0 & 0 & 1 & \cdots & 0 \\\ 
    \vdots & \vdots & \vdots & \ddots & \vdots \\\ 
    0 & 0 & 0 & \cdots & 1
    \end{pmatrix}
    \label{eq:identity}
\end{equation}

## Inverse

If a square matrix $$\mat{A}$$ has an inverse $$\mat{A}^{-1}$$, then
\begin{equation}
  \mat{A}^{-1} \vdot \mat{A} = \mat{I} = \mat{A} \vdot \mat{A}^{-1}
\end{equation}

If $$\mat{A}$$ transforms a column vector $$\vb{x}$$ to a new column vector $$\vb{y} = \mat{A} \vdot \vb{x}$$, the inverse matrix allows us to recover $$\vb{x}$$ from  $$\vb{y}$$ via $$\vb{x} = \mat{A}^{-1} \vdot \vb{y}$$ since
\begin{equation}
  \mat{A}^{-1} \vb{y} = \mat{A}^{-1} \vdot (\mat{A} \vdot \vb{x}) = (\mat{A}^{-1} \vdot \mat{A}) \vdot \vb{x} =
   \mat{I} \vdot \vb{x} = \vb{x}
\end{equation}
The existence of an inverse implies that operating with $$\mat{A}$$ on a vector does not entail the loss of information; that is, the matrix has a trivial **nullspace**, which means that its rows (and columns) are linearly independent. It usually isn't obvious by inspection whether a square matrix has an inverse (that its rows are linearly independent). If one or more rows can be expressed as the linear combination of other rows, then the matrix is **singular**, its **determinant** vanishes, and it does not have an inverse. 

You can use [Gauss-Jordan elimination](LA-GaussJordan.md) to compute the inverse of a square matrix (provided it has one).


Besides the identity matrix, there are a number of important classes of square matrices that arise in physics:

## Hermitian Matrices

A **Hermitian matrix** is a complex matrix equal to its conjugate transpose: $$\mat{H} = \mat{H}^*$$.

+ In matrix mechanics, Hermitian matrices represent physically observable quantities (e.g., angular momentum, the hamiltonian (energy), etc.). The matrix representing the $$z$$ component of spin angular momentum of a spin-1/2 particle, in the basis of $$\ket{\uparrow}, \ket{\downarrow}$$ along $$z$$ is
\\[
  \hat{S}_z \longrightarrow
  \frac{\hslash}{2} \begin{pmatrix}
    1 & 0 \\\ 0 & -1
  \end{pmatrix}
\\]
Note that the “hat” on $$S_z$$ indicates that it is an operator; it operates on a vector in the space of the spin-1/2 particle and produces another vector in the space.

+ Hermitian matrices are diagonalizable.
+ Hermitian matrices have real eigenvalues.

## Normal Matrices

A **normal matrix** commutes with its conjugate transpose: $$\mat{A}^{*\mathrm{T}} \vdot \mat{A} = \mat{A} \vdot \mat{A}^{*\mathrm{T}}$$.

## Unitary Matrices

A **unitary matrix** is a complex square matrix whose inverse is equal to its conjugate transpose: $$\mat{U}^{-1} = \mat{U}^*$$. 


+ A unitary matrix that represents the rotation of a spin-1/2 particle through angle $$\phi$$ around the $$z$$ axis, expressed in the basis of $$\ket{\uparrow}, \ket{\downarrow}$$ along $$z$$ is
\\[
  \hat{R}(\phi \vu{z}) \longrightarrow \begin{pmatrix}
    e^{-i\phi/2} & 0 \\\ 
    0 & e^{i\phi/2}
  \end{pmatrix}
\\]
+ Unitary matrices are one type of normal matrices. They preserve lengths and inner products.
+ $$\mat{U} = e^{i \mat{H}}$$, where $$\mat{H}$$ is a Hermitian matrix. The meaning of the exponential of an operator derives from the exponential series:
\begin{equation}
  e^{i\mat{H}} = \mat{I} + i\mat{H} + \frac{i^2}{2!} \mat{H}\vdot \mat{H} + \frac{i^3}{3!} \mat{H}\vdot\mat{H}\vdot\mat{H} + \cdots
\end{equation}

## Orthogonal Matrices

An orthogonal matrix satisfies
\begin{equation}
  \mat{O}^{\rm T} \vdot \mat{O} = \mat{O} \vdot \mat{O}^{\rm T} = \mat{I}
\end{equation}
where $$\mat{O}^{\rm T}$$ is the transpose of $$\mat{O}$$, which interchanges rows and columns. For an orthogonal matrix, therefore,
\begin{equation}
  \mat{O}^{\rm T} = \mat{O}^{-1}
\end{equation}

The determinant of an orthogonal matrix is either $$+1$$ or $$-1$$. Orthogonal matrices with determinant $$+1$$ are called **special orthogonal matrices** [the group of all such matrices of dimension $$n$$ is notated $$\mat{SO}(n) $$] and they correspond to rotations in $$\mathbb{R}^n$$. Orthogonal matrices with determinant equal to $$-1$$ combine rotations with an inversion through the origin. They reverse the handedness of the underlying coordinate system.

Orthogonal matrices:

+ preserve lengths of vectors
+ preserve the inner product between two vectors


### Rotation Matrices

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

