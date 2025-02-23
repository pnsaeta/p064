{:menu FO}

# Contour Integration

* toc
{:toc}

We saw in [the page on Complex Variables](FO-ComplexVariables.md) that the integral around a closed contour on the complex plane may be evaluated by summing the residues of the enclosed poles. Let’s check this out by evaluating the following integral:
\begin{equation}
  I = \int_{-\infty}^{\infty} \frac{1}{1 + x^2}\dd{x}
\end{equation}
This is not an integral for which we require the methods of contour integration; we could simply use a $$u$$ substitution, letting $$x = \tan u$$, so that $$\dd{x} = \sec^2{u}\dd{u}$$ to transform the integral to
\begin{equation}
  I = \int_{-\pi/2}^{\pi/2} \frac{1}{1 + \tan^2 u} \sec^2{u}\dd{u} = \int_{-\pi/2}^{\pi/2} \dd{u} = \pi
\end{equation}

Can we get the same result from contour integration?

We need to find a way to close the contour that includes the entire real axis, but needs to somehow get from $$x = \infty$$ to $$x = -\infty$$.