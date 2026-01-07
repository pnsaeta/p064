{:menu LA}


# Square Matrices

* toc
{:toc}

## Categories
Square matrices have a number of interesting properties and deserve special attention. An $$N \times N$$ square matrix maps an $$N$$-dimensional vector into another $$N$$-dimensional vector. Several types of square matrices have special properties:

- an **identity** matrix $$\mat{I}$$ maps a vector to itself, much as multiplying by the number 1 leaves another value unchanged.
- the **inverse** of a square matrix *undoes* the transformation that the matrix causes: $$\mat{A}^{-1} \vdot \mat{A} = \mat{I}$$. Applying first one and then the other yields the original vector. Most matrices do not have an inverse; only those whose rows are linearly independent do.
- the **transpose** of a matrix is the matrix yielded by exchanging rows and columns: $$(\mat{A}^{\mathrm{T}})_{ij} = \mat{A}_{ji}$$.
- an **orthogonal** matrix $$\mat{O}$$ satisfies $$\trans{O} \vdot \mat{O} = \mat{O} \vdot \trans{O} = \mat{I}$$. Orthogonal matrices rotate and/or reflect vectors, preserving their length.
- a **rotation** matrix $$\mat{R}_{\vb{u}}(\theta)$$ rotates a vector through angle $$\theta$$ around the axis specified by the unit vector $$\vb{u}$$. If the space is real, then a rotation matrix is an orthogonal matrix. If the space is complex, a rotation matrix is **unitary** (see below).
- a **Hermitian** matrix $$\mat{H}$$ is a complex valued matrix that is equal to its complex conjugate transpose: $$\mat{H} = (\mat{H}^*)^{\mathrm{T}} = \hc{H}$$. Hermitian matrices have real eigenvalues and orthogonal eigenvectors.
- a **normal** matrix commutes with its conjugate transpose, $$\mat{N}\vdot\hc{N} = \hc{N}\vdot\mat{N}$$, which means that you get the same matrix regardless of the order in which you multiply them.
- the inverse of a **unitary** matrix is equal to its conjugate transpose: $$\mat{U}^{-1} = \hc{U}$$. Unitary matrices preserve the length of a vector. The time evolution operator in quantum mechanics may be represented by a unitary matrix whose matrix elements generally depend on time $$t$$.

### Question

1. Consider the matrices
\\[
  \mat{A} = \begin{pmatrix}
    1 & 2i \\\
    2i & 3
  \end{pmatrix}
  \qquad
  \mat{B} = \begin{pmatrix}
    1 & 2i \\\
    -2i & 4
  \end{pmatrix}
  \qquad
  \mat{C} = \begin{pmatrix}
    \sqrt{3}/2 & 1/2 \\\
    -1/2 & \sqrt{3}/2
    \end{pmatrix}
\\]
Which of these are (a) orthogonal? (b) Hermitian? (c) Unitary?

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

## Determinants

You undoubtedly already know what a determinant is, and how you can work it out using minors, but allow me to make a couple of definitions.

- Each contribution to the determinant of an $$N$$-dimensional matrix is the product of $$N$$ terms, one from each column and row.
- There are $$N!$$ such contributions, since there are $$N$$ choices for the column in the first row, $$N-1$$ choices for the column in the second row, etc.
- We can represent a particular ordering with the indices of the successive columns. For example, 1324 would mean to multiply $$a_{11} a_{23} a_{32} a_{44}$$ for a matrix whose elements are $$a_{ij}$$.
- Starting from the ordering $$123\cdots$$ for the columns, every other ordering can be constructed by pairwise exchange of two elements. For example, to get to 1423 from the reference ordering 1234, we could proceed $$1234 \to 1324 \to 1423$$, which took two exchanges. All possible permutations take either an even or odd number of exchanges.
- The determinant is the sum of all $$N!$$ N-term products, which are counted positive for **even** permutations and negative for **odd** permutations.
- The **Levi-Civita symbol** $$\varepsilon_{ijklm\cdots}$$ for $$N$$ elements has $$N$$ subscripts (indices) and is defined by
\begin{equation}
  \varepsilon_{ijk\cdots} = \begin{cases}
    1 & ijk\cdots = 123\cdots \text{ and even permutations} \\\
    -1 & ijk\cdots = 132\cdots \text{ and odd permutations of } 123\cdots \\\
    0 & \text{if any index is repeated}
  \end{cases}
\end{equation}
- The determinant is then defined by
\begin{equation}\label{eq:determinant}
    D = \sum_{ijk\cdots} (\varepsilon_{ijk\cdots}) a_{1i} a_{2j} a_{3k} \cdots
\end{equation}

### Properties of Determinants

- Exchanging two rows in a matrix changes the sign of the value of its determinant.
- Exchanging two columns in a matrix changes the sign of the value of its determinant.
- Multiplying one row of a matrix by a constant $$\alpha$$ multiplies the determinant by $$\alpha$$.
- Multiplying on row of a matrix by a constant $$\alpha$$ and adding the result to another row leaves the determinant unchanged.
- Multiplying a matrix by $$\alpha$$ multiplies the determinant by $$\alpha^N$$: $$\det(\alpha \mat{A}) = \alpha^n \det(\mat{A})$$.
- The determinant of a product is the product of determinants: $$\det(\mat{A} \mat{B}) = \det(\mat{A}) \det(\mat{B})$$.
- The determinant of the inverse is the reciprocal of the determinant: $$\det(\mat{A}^{-1}) = \frac{1}{\det{\mat{A}}} $$.

## Trace

The trace of a square matrix is the sum of the elements on the main diagonal:
\\[
    \text{Tr } \mat{A} = \sum_{j=1}^N a_{jj}
\\]
The trace has the property
\\[
\text{Tr }(\mat{A \cdot B}) = \text{Tr }(\mat{B \cdot A})
\\]

Next: [Gauss-Jordan Elimination](LA-GaussJordan.md)
