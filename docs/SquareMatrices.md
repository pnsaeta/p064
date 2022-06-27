# Square Matrices

Square matrices have a number of interesting properties and deserve special attention.

## Identity Matrix

The identity matrix has ones along the main diagonal and zeros everywhere else:
\begin{equation}
  \mat{I} = \begin{pmatrix}
    1 & 0 & 0 & \cdots & 0 \\\\\\ 
    0 & 1 & 0 & \cdots & 0 \\\\\\ 
    0 & 0 & 1 & \cdots & 0 \\\\\\ 
    \vdots & \vdots & \vdots & \ddots & \vdots \\\\\\ 
    0 & 0 & 0 & \cdots & 1
    \end{pmatrix}
    \label{eq:identity}
\end{equation}

## Inverse

If a square matrix $$\mat{A}$$ has an inverse $$\mat{A}^{-1}$$, then
\begin{equation}
  \mat{A}^{-1} \mat{A} = \mat{I} = \mat{A} \mat{A}^{-1}
\end{equation}

If $$\mat{A}$$ transforms a column vector $$\vb{x}$$ to a new column vector $$\vb{y} = \mat{A}\vb{x}$$, the inverse matrix allows us to recover $$\vb{x}$$ from  $$\vb{y}$$ via $$\vb{x} = \mat{A}^{-1} \vb{y}$$ since
\begin{equation}
  \mat{A}^{-1} \vb{y} = \mat{A}^{-1} (\mat{A} \vb{x}) = (\mat{A}^{-1} \mat{A}) \vb{x} =  \mat{I} \vb{x} = \vb{x}
\end{equation}
The existence of an inverse implies that operating with $$\mat{A}$$ on a vector does not entail the loss of information; that is, the matrix lacks a **nullspace**, which means that its rows are linearly independent. It usually isn't obvious by inspection whether a square matrix has an inverse (that its rows are linearly independent). If one or more rows can be expressed as the linear combination of other rows, then the matrix is **singular**, its **determinant** vanishes, and it does not have an inverse.

You can use [Gauss-Jordan elimination](GaussJordan.md) to compute the inverse of a square matrix (provided it has one).

## Special Square Matrices

Besides the identity matrix, there are a number of important classes of square matrices that arise in physics:

### Hermitian
A **Hermitian matrix** is a complex matrix equal to its conjugate transpose: $$\mat{H} = \mat{H}^*$$.

+ In matrix mechanics, Hermitian matrices represent physically observable quantities (e.g., angular momentum, the hamiltonian (energy), etc.). The matrix representing the $$z$$ component of spin angular momentum of a spin-1/2 particle, in the basis of $$\ket{\uparrow}, \ket{\downarrow}$$ along $$z$$ is
\\[
  \hat{S}_z \longrightarrow
  \frac{\hslash}{2} \begin{pmatrix}
    1 & 0 \\\ 0 & -1
  \end{pmatrix}
\\]
+ Hermitian matrices are diagonalizable.
+ Hermitian matrices have real eigenvalues.

### Normal
 A **normal matrix** commutes with its conjugate transpose: $$\mat{A}^* \mat{A} = \mat{A} \mat{A}^*$$.

### Unitary
A **unitary matrix** is a complex square matrix whose inverse is equal to its conjugate transpose: $$\mat{U}^{-1} = \mat{U}^*$$. 


+ A unitary matrix that represents the rotation of a spin-1/2 particle through angle $$\phi$$ around the $$z$$ axis, expressed in the basis of $$\ket{\uparrow}, \ket{\downarrow}$$ along $$z$$ is
\\[
  \hat{R}(\phi \vu{z}) \longrightarrow \begin{pmatrix}
    e^{-i\phi/2} & 0 \\\ 
    0 & e^{i\phi/2}
  \end{pmatrix}
\\]
+ Unitary matrices are one type of normal matrices. They preserve lengths and inner products.
+ $$\mat{U} = e^{i \mat{H}}$$, where $$\mat{H}$$ is a Hermitian matrix.

### Orthogonal

An orthogonal matrix satisfies
\begin{equation}
  \mat{O}^{\rm T} \mat{O} = \mat{O} \mat{O}^{\rm T} = \mat{I}
\end{equation}
where $$\mat{O}^{\rm T}$$ is the transpose of $$\mat{O}$$, which interchanges rows and columns. For an orthogonal matrix, therefore,
\begin{equation}
  \mat{O}^{\rm T} = \mat{O}^{-1}
\end{equation}

The determinant of an orthogonal matrix is either $$+1$$ or $$-1$$. Orthogonal matrices with determinant $$+1$$ are called **special orthogonal matrices** [the group of all such matrices of dimension $$n$$ is notated $$\mat{SO}(n) $$] and they correspond to rotations in $$\mathbb{R}^n$$. Orthogonal matrices with determinant equal to $$-1$$ combine rotations with an inversion through the origin. They reverse the handedness of the underlying coordinate system.

Orthogonal matrices:

+ preserve lengths of vectors
+ preserve the inner product between two vectors