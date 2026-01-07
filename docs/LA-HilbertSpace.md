{:menu LA}


# Hilbert Space

A **Hilbert space** is a vector space with an inner product that is used to define a distance function for which it is a complete metric space. That is, the “length” of a vector in the space is given by $$\parallel\vb{v}\parallel = \sqrt{\ev{\vb{v},\vb{v}}}$$ and the distance between two vectors is defined by $$\parallel \vb{v-w} \parallel = \sqrt{\ev{\vb{v-w}, \vb{v-w}}}$$. ([See here](LA-LinearAlgebra.md#complex-spaces) for the definition of inner product for vector spaces over the field of complex numbers.)

The meaning of a **complete metric space** has to do with with limiting sequences of vectors: if a series of vectors, $$\displaystyle \sum_{k=0}^\infty \vb{v}_k$$ converges absolutely — meaning that $$\displaystyle\sum_{k=0}^\infty \parallel \vb{v}_k \parallel < \infty$$ — then the partial sums converge to an element in the Hilbert space.

What is an example of a Hilbert space? Suppose that $$H$$ is the space of all square-integrable one-dimensional real functions of a real variable. That is, the elements $$f$$ of the space $$H$$ satisfy
\begin{equation}\label{eq:square-integrable}
  \int_{-\infty}^{\infty} [f(x)]^2 \dd{x} < \infty
\end{equation}
These functions must die away sufficiently rapidly as $$|x| \to \infty$$ for the integral to exist, and this property ensures that the inner product of two such functions remains a function in the Hilbert space. This means that linear combinations of these vectors in the space remain square-integrable and form (normalizable) vectors in the space.

A Hilbert space is **spanned** by a set of basis vector, $$\ket{\varphi_j}$$ for $$j = 1, 2, \ldots, $$. It may either by finite-dimensional or infinitedimensional. All vectors in the space may be expressed as a linear combination of the basis vectors. That is, the space is **complete**.
