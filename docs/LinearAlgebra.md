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

# Linear Algebra

[Back to the top](index.md)

* toc
{:toc}

## Notation

A “delightful” bug (feature?) of mathematical physics is the different notations used to describe identical mathematical systems/situations. In physics, we are wont to represent a quantity with magnitude and direction, such as a force $$\vb{F}$$ in either boldface or with an arrow over it ($$\va{F}$$). Mathematicians often prefer to use a component notation $$(F_1, F_2, F_3)$$ to represent the same thing. Each strategy has its pros and cons. The problem with the component notation is that it implicitly assumes a particular basis—which is typically **not** made explicit. Thus, we are “invited” to guess that $$F_1$$ is the component of $$F$$ in the $$x$$ direction, but unless this choice is stated explicitly, we can't really be sure. The “physics” notation $$\vb{F}$$ implies that the quantity $$F$$ has both a magnitude and a direction, but declines to state explicitly what its components may be. After all, the direction of the force exists *independent* of the choice of basis vectors we make to describe it. Fundamentally, north is north, even if we orient our coordinate system in some cockamaimie direction. Hence, much of physics is written in coordinate-free notation that emphasizes that vectors have magnitude and direction, rather than that they have representations in various bases.

## Linear Operators

A linear operator $$\hat{A}$$ has the following behavior
\begin{equation}\label{eq:linear-operator}
  \hat{A}(\alpha \vb{x} + \beta \vb{y}) = \alpha \hat{A}\vb{x} + \beta \hat{A}\vb{y}
\end{equation}
In this expression, $$\alpha$$ and $$\beta$$ are scalar values (either real numbers or complex numbers) and $$\vb{x}$$ and $$\vb{y}$$ are $$N$$-dimensional vectors. The operator $$\hat{A}$$ transforms a vector in an $$N$$-dimensional space into another vector in the same $$N$$-dimensional space. Equation \ref{eq:linear-operator} says that you get the same result whether you combine vectors and then transform with the operator as when you transform the vectors separately and then combine the results. Why is this interesting?

Many physical quantities have this property. In classical mechanics, some linear operators are:

+ translation by a fixed displacement, $$\hat{T}(\vb{a})$$, which takes $$\vb{r} \to \vb{r} + \vb{a}$$, but leaves momentum unchanged.
+ Galilean transformations, $$\hat{G}(\vb{v})$$, which take $$\vb{r} \to \vb{r} + \vb{v} t$$ and $$\vb{p} \to \vb{p} + m\vb{v}$$.
+ time reversal, $$\hat{T}$$, which takes $$\vb{r}(t) \to \vb{r}(-t)$$ and $$\vb{p}(t) \to -\vb{p}(-t)$$.

Linear operators are more much important in quantum mechanics. These act on a quantum state (vector), $$\ket{\psi}$$ and produce another state (vector) $$\ket{\varphi}$$ in the same vector space over the field of complex numbers. (In quantum mechanics, we represent state vectors as “kets” with the notation $$\ket{\psi}$$, which is a notation due to Paul Dirac. Indeed, every physically observable quantity corresponds to a special kind of linear operator, called a Hermitian operator, whose properties we will define and explore below.

+ rotation through angle $$\theta$$ around the $$z$$ axis, $$\hat{R}(\theta \vu{z})$$
+ the hamiltonian, $$\hat{H}$$, which acts on a state $$\ket{\psi}$$ to weight its components by their respective energies. If $$\ket{\psi}$$ is an eigenstate (eigenvector) of the hamiltonian, then $$\hat{H}\ket{\psi} = E \ket{\psi}$$.

## Inner Products

The inner product of two vectors, $$\vb{a}$$ and $$\vb{b}$$, requires us (roughly speaking) to multiply corresponding components and then add up the resulting products. If the vectors live in $$\mat{R}^n$$, then the multiplication is the normal one you expect:
\begin{equation}\label{eq:real-inner-product}
  \vb{a} \vdot \vb{b} = (\vb{a}, \vb{b}) = \sum_{i=1}^N a_i b_i
\end{equation}

From a matrix standpoint, the inner product of two vectors is represented by the matrix multiplication of the transpose of one by the other:
\\[
  \vb{a} \vdot \vb{b} = 
  \begin{pmatrix}
    a_1 & a_2 & a_3 & \cdots
  \end{pmatrix} \vdot \begin{pmatrix}
    b_1 \\\ b_2 \\\ b_3 \\\ \vdots
  \end{pmatrix}
\\]

Note that this operation only makes sense provided that both vectors have the same dimension.

The magnitude of a vector having such an inner product is given by
\begin{equation}\label{eq:real-mag}
  |\vb{a}| = \sqrt{\vb{a} \vdot \vb{a}} = \qty(\sum_{i=1}^N a_i^2)^{1/2}
\end{equation}
which is just what we’d expect from the Pythagorean theorem.

### Complex spaces

On the other hand, if the vectors inhabit a vector space over the field of complex numbers (as in quantum mechanics), the inner product is defined slightly differently:
\begin{equation}\label{eq:complex-inner-product}
  \braket{a}{b} = \sum_{i=1}^N (a_i)^* b_i
\end{equation}
where the star indicates complex conjugation. This definition ensures that the magnitude squared of any state vector is a nonnegative real number: 
\begin{equation}\label{eq:c-magnitude}
    \braket{a}{a} = \sum_{i=1}^N a_i^* a_i = \sum_{i=1}^N |a_i^2|
\end{equation}

It is common in physics to use the same notation for the magnitude of a vector as for the absolute value of a real or complex number: 
\\[
   |x|, |\vb{a}| \qqtext{(physics)} \qqtext{vs} |x|, ||\vb{a}|| \qqtext{(math)}
\\]
Because physicists habitually use notation that distinguishes vectors from scalars and matrices, the double pipes are unnecessary; since math frequently does not, using the double pipes for **norm** helps remind the reader of the meaning of the vector whose norm is being referenced.


### Vector Spaces over the Field of Complex Numbers

The “length” of a vector should be a non-negative real number. For this notion to work in vector spaces over the field of complex numbers, we must modify the definition of the inner product to require that the first vector's values be complex conjugated. In such cases, it is often convenient to define a **dual space** with the following property. If the components of vector $$\ket{a}$$ in some basis are $$a_1$$, $$a_2$$, $$\ldots$$, then the components of the dual vector $$\bra{a}$$ in the same basis are $$a_1^*$$, $$a_2^*$$, $$\ldots$$. Furthermore, we can represent the ket vector $$\ket{a}$$ in this basis as a column vector,
\begin{equation}
  \ket{a} \longrightarrow \pmatrix{a_1 \\\  a_2 \\\ \vdots \\\ a_N}
\end{equation}
and the “bra” vector (the dual) as a row vector
\begin{equation}
  \bra{a} \longrightarrow \pmatrix{a_1^* & a_2^* & \cdots & a_N^*}
\end{equation}

so that the inner product is achieved by standard matrix multiplication of bra and ket:
\begin{equation}
  \braket{a}{a} \longrightarrow \pmatrix{a_1^* & a_2^* & \cdots & a_N^*}
    \vdot \pmatrix{a_1 \\\  a_2 \\\ \vdots \\\ a_N} = \sum_{i=1}^N |a_i|^2
\end{equation}
which is a manifestly nonnegative real number.

## Linear Independence

Two vectors $$\vb{a}$$ and $$\vb{b}$$ are linearly independent if and only if
\begin{equation}
  \vb{a} \cdot \vb{b} = |\vb{a}| |\vb{b}| \cos\theta_{ab} < |\vb{a}| |\vb{b}|
\end{equation}
which means that they are not colinear. In general, a vector space of dimension $$D$$ is spanned by 
$$D$$ linearly independent vectors, which are often chosen to be unit vectors in
each of the Cartesian directions: $$e_1 = (1,0,0,\ldots)$$, $$e_2 = (0, 1, 0, \ldots)$$, etc.

## Outer Products

The inner product described above takes two vectors of equal dimension and contracts them to produce a scalar. In matrix language, it is the product of the transpose of the first vector (converting a column vector to a row vector) by the second. What happens if we let the first vector remain a column vector but "contract" it with the transpose of the second vector? That is, take
\\[
  \mat{M} = \begin{pmatrix} a_1 \\\ a_2 \\\ \vdots \\\ a_m \end{pmatrix} \vdot
    \begin{pmatrix} b_1 & b_2 & \cdots & b_n \end{pmatrix}
    =
    \begin{pmatrix}
      a_1 b_1 & a_1 b_2 & \cdots & a_1 b_n \\\ 
      a_2 b_1 & a_2 b_2 & \cdots & a_2 b_n \\\ 
      \vdots & \vdots & \ddots & \vdots \\\ 
      a_m b_1 & a_m b_2 & \cdots & a_m b_n
    \end{pmatrix}
  \\]
This is called the **outer product** of the two vectors and produces a rectangular matrix with $$m$$ rows and $$n$$ columns.