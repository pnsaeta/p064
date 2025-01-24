{:menu LA}


# Square Matrices

* toc
{:toc}

Square matrices have a number of interesting properties and deserve special attention. An $$N \times N$$ square matrix maps an $$N$$-dimensional vector into another $$N$$-dimensional vector. Several types of square matrices have special properties: 

- an **identity** matrix $$\mat{I}$$ maps a vector to itself, much as multiplying by the number 1 leaves another value unchanged.
- the **inverse** of a square matrix *undoes* the transformation that the matrix causes: $$\mat{A}^{-1} \vdot \mat{A} = \mat{I}$$. Applying first one and then the other yields the original vector. Most matrices do not have an inverse; only those whose rows are linearly independent do.
- the **transpose** of a matrix is the matrix yielded by exchanging rows and columns: $$(\mat{A}^{\mathrm{T}})_{ij} = \mat{A}_{ji}$$.
- an **orthogonal** matrix $$\mat{O}$$ satisfies $$\trans{O} \vdot \mat{O} = \mat{O} \vdot \trans{O} = \mat{I}$$. Orthogonal matrices rotate and/or reflect vectors, preserving their length.
- a **rotation** matrix $$\mat{R}_{\vb{u}}(\theta)$$ rotates a vector through angle $$\theta$$ around the axis specified by the unit vector $$\vb{u}$$. If the space is real, then a rotation matrix is an orthogonal matrix. If the space is complex, a rotation matrix is **unitary** (see below). 
- a **Hermitian** matrix $$\mat{H}$$ is a complex valued matrix that is equal to its complex conjugate transpose: $$\mat{H} = (\mat{H}^*)^{\mathrm{T}} = \hc{H}$$. Hermitian matrices have real eigenvalues and orthogonal eigenvectors.
- a **normal** matrix commutes with its conjugate transpose, $$\mat{N}\vdot\hc{N} = \hc{N}\vdot\mat{N}$$, which means that you get the same matrix regardless of the order in which you multiply them.
- the inverse of a **unitary** matrix is equal to its conjugate transpose: $$\mat{U}^{-1} = \hc{U}$$. Unitary matrices preserve the length of a vector. The time evolution operator in quantum mechanics may be represented by a unitary matrix whose matrix elements generally depend on time $$t$$. 


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
  \mat{A}^{-1} \vdot \vb{y} = \mat{A}^{-1} \vdot (\mat{A} \vdot \vb{x}) = (\mat{A}^{-1} \vdot \mat{A}) \vdot \vb{x} =
   \mat{I} \vdot \vb{x} = \vb{x}
\end{equation}
The existence of an inverse implies that operating with $$\mat{A}$$ on a vector does not entail the loss of information; that is, the matrix has a trivial **nullspace**, which means that its rows (and columns) are linearly independent. It usually isn't obvious by inspection whether a square matrix has an inverse (that its rows are linearly independent). If one or more rows can be expressed as the linear combination of other rows, then the matrix is **singular**, its **determinant** vanishes, and it does not have an inverse.

You can use [Gauss-Jordan elimination](LA-GaussJordan.md) to compute the inverse of a square matrix (provided it has one).

## Hermitian Matrices

A **Hermitian matrix** is a complex matrix equal to its conjugate transpose: $$\mat{H} = \widetilde{\mat{H}} = (\mat{H}^{*})^{\mathrm{T}}$$.

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

A **normal matrix** commutes with its conjugate transpose: $$\widetilde{\mat{A}} \vdot \mat{A} = \mat{A} \vdot \widetilde{\mat{A}} $$.

## Unitary Matrices

A **unitary matrix** is a complex square matrix whose inverse is equal to its conjugate transpose: $$\mat{U}^{-1} = \widetilde{\mat{U}}$$. 


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

## Miscellany

- $$\det(\alpha \mat{A}) = \alpha^n \det(\mat{A})$$
- $$\det(\mat{A} \mat{B}) = \det(\mat{A}) \det(\mat{B})$$
- $$\det(\mat{A}^{-1}) = \frac{1}{\det{\mat{A}}} $$
- $$\mathrm{trace}(\mat{A B}) = \mathrm{trace}(\mat{B A})$$