{:menu LA}


# Diagonalization

* toc
{:toc}

[Back to the top](LA-LinearAlgebra.md)

A **similarity transformation** of a square matrix $$\mat{A}$$ is a product of the form
\\[
  \mat{D} = \mat{S}^{-1} \vdot \mat{A} \vdot \mat{S}
\\]
for some square matrix $$\mat{S}$$ such that $$\mat{D}$$ is a diagonal matrix (i.e. has nonzero elements only along the main diagonal). A similarity transformation represents a change of basis (a rotation) that allows the effect of $$\mat{A}$$ to be expressed in simplest terms.

Applying $$\mat{S}^{-1}$$ to the right and $$\mat{S}$$ to the left of this equation gives
\\[
  \mat{S} \vdot \mat{D} \vdot \mat{S}^{-1} = \mat{A}
\\]
Evidently, $$\mat{D}$$ expresses the same action as $$\mat{A}$$, but in a basis where its only effect is to stretch each dimension by a (potentially) different amount. The matrix $$\mat{S}^{-1}$$ transforms the basis of $$\mat{A}$$ into the “natural” diagonal basis of the transformation, and $$\mat{S}$$ transforms back from this basis to the basis of $$\mat{A}$$.

A similarity transformation preserves the determinant of a matrix.

## Eigenvalues and Eigenvectors

An $$n$$-dimensional square matrix $$\mat{A}$$ transforms a vector in $$\mathbb{R}^n$$ to another vector in $$\mathbb{R}^n$$; in general, the transformed vector points in a different direction than the original vector and has different magnitude. However, an eigenvector satisfies
\\[
    \mat{A} \vdot \vb{x} = \lambda \vb{x}
\\]
for some *scalar* **eigenvalue** $$\lambda$$. That is, the action of transformation $$\mat{A}$$ on an **eigenvector** $$\vb{x}$$ produces a copy of $$\vb{x}$$ scaled by the **eigenvalue** $$\lambda$$. Diagonalizing a matrix $$\mat{A}$$ consists in finding the similarity transformation that puts all its eigenvalues along the main diagonal.

Certain kinds of matrices are guaranteed to be diagonalizable and to have a set of **eigenvectors** that span their $$n$$-dimensional space. These include

+ real symmetric matrices
+ Hermitian (complex self-adjoint) matrices ([see below](#Hermitian-operators))

Eigenvectors corresponding to different eigenvalues are guaranteed to be orthogonal:
\begin{align}
  \mat{H}\vdot \vb{x}_1 &= \lambda_1 \vb{x_1} &\qquad \vb{x}_2\vdot\mat{H}\vdot\vb{x}_1 &= \lambda_1 \vb{x}_2 \vdot \vb{x}_1 \\\ 
  \mat{H}\vdot \vb{x}_2 &= \lambda_2 \vb{x_2} &\qquad \vb{x_1}\vdot\mat{H}\vdot\vb{x_2} &= \lambda_2 \vb{x}_1 \vdot \vb{x}_2
\end{align}
If $$\mat{H}$$ is a real symmetric matrix, then subtracting the two rows gives
\\[
    \vb{x}_2\vdot\mat{H}\vdot\vb{x}_1 - \vb{x_1}\vdot\mat{H}\vdot\vb{x_2} = (\lambda_1-\lambda_2) \vb{x}_1 \vdot \vb{x_2}
\\]
But $$(\vb{x}_2 \vdot \mat{H} \vdot \vb{x}_1)^{\rm T} = \vb{x}_1 \vdot \mat{H}^{\rm T} \vdot \vb{x}_2 =
 \vb{x}_1 \vdot \mat{H} \vdot \vb{x}_2 $$ since $$\mat{H}$$ is symmetric. Therefore, the left-hand side vanishes, and since $$\lambda_1 \ne \lambda_2$$, it must be true that $$\vb{x}_1\vdot\vb{x}_2 = 0$$. So, *eigenvectors corresponding to distinct eigenvalues are orthogonal*. The proof for Hermitian matrices is similar.

Since a scalar multiple of an eigenvector is also an eigenvector, it is possible to find a set of orthonormal eigenvectors that span the vector space of real symmetric matrices and also of Hermitian matrices.

## Positive Definite Matrices

A symmetric square matrix $$\mat{A}$$ is **positive definite** if 
\\[
    \vb{x}^{\rm T}\vdot\mat{A}\vdot\vb{x} \ge 0
\\]
for all vectors $$\vb{x}$$. [If $$\mat{A}$$ is Hermitian, then the transpose operation implies complex conjugation.] Such matrices have nonnegative real eigenvalues. The proof is straightforward. Suppose that $$\vb{x}$$ is an eigenvector with eigenvalue $$\lambda$$. Then
\\[
    \vb{x}^{\rm T} \vdot \mat{A} \vdot \vb{x} = \vb{x}^{\rm T} \vdot \lambda \vb{x} = \lambda | \vb{x} |^2
\\]
Taking the transpose of this equation gives
\\[
    \qty(\vb{x}^{\rm T} \vdot \mat{A} \vdot \vb{x})^{\rm T} = \vb{x}^{\rm T} \vdot \mat{A}^\rm {T} \vdot \qty(\vb{x}^{\rm T})^{\rm T} = \vb{x}^{\rm T} \vdot \mat{A} \vdot \vb{x} = \lambda |\vb{x}|^2
\\]
The norm of a vector is positive-definite, and by assertion, so is $$\vb{x}^{\rm T}\vdot\mat{A}\vdot\vb{x}$$. Therefore, $$\lambda \ge 0$$. Once again, the proof for Hermitian matrices is similar.

## Hermitian Operators

Let’s practice with Dirac notation. Recall that if $$\op{A}\ket{a} = \ket{b}$$

## Physics Example

What is a physical example of a positive-definite matrix? Consider the kinetic energy of a rotating rigid body. Choosing an origin on the axis of rotation, the velocity of any point on the body is given by
\\[
    \vb{v}\_i = \vb*{\omega}\cross\vb{r}\_i
\\]

The kinetic energy of a mass $$m_i$$ at $$\vb{r}_i$$ is 
\\[
    K = \frac12 m\_i \vb{v}\_i \vdot \vb{v}\_i =
     \frac12 m\_i (\vb\*{\omega}\cross\vb{r}\_i) \vdot
     (\vb\*{\omega}\cross\vb{r}\_i)
\\]
Let us decompose $$\vb{r}_i$$ into its components parallel and perpendicular to $$\vb*{\omega}$$:
\\[
    \vb{r}\_i = \vb{r}\_i^{\parallel} + \vb{r}\_i^{\perp}
\\]
The magnitude of the cross product with $$\vb*{\omega}$$ is $$\omega r_i^{\perp} = \omega |\vb{r}_i - \vb{r}_i^{\parallel}|$$, so the magnitude squared is
\\[
    (\vb\*{\omega}\cross\vb{r}\_i) \vdot (\vb\*{\omega}\cross\vb{r}\_i)
    = \omega^2 r\_i^2 - (\vb*{\omega}\vdot\vb{r}\_i)^2
    = \vb\*{\omega}^{\rm T} \vdot (r\_i^2 \mat{I} - \vb{r}\_i \vdot \vb{r}\_i^{\rm T}) \vdot \vb\*{\omega}
\\]
Therefore, we can express the kinetic energy of the rotating rigid body as
\\[
    K = \frac12
    \begin{pmatrix}
    \omega_x & \omega_y & \omega_z
    \end{pmatrix}
    \vdot
    \underbrace{
      \qty[
    \sum\_i
    m\_i
    \begin{pmatrix}
      r\_i^2 - x\_i^2 & -x\_i y\_i & -x\_i z\_i \\\ 
      -y\_i x\_i & r\_i^2 - y\_i^2 & -y\_i z\_i \\\ 
      -z\_i x\_i & -z\_i y\_i  & r\_i^2 - z\_i^2 
    \end{pmatrix}
    ]
    }\_{\mat{J}}
    \vdot
    \begin{pmatrix}
    \omega\_x \\\ \omega\_y \\\ \omega\_z
    \end{pmatrix}
\\]
where $$\mat{J}$$ represents the **inertia tensor** of the rigid body. Since the contribution to the kinetic energy of each mass point $$m_i$$ is nonnegative, the symmetric matrix of the inertia tensor is positive definite (despite the impressive number of evident minus signs!).

The structure of the inertia tensor makes it possible to show that we can always find a body-centered coordinate system in which the matrix is diagonal; because it is also positive definite, the eigenvalues along the diagonal must all be nonnegative. 

