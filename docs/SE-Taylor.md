{:menu SE}

# Taylor Series

* toc
{:toc}

Taylor's expansion is a way of approximating a function $$f(x)$$ in the neighborhood of a point $$x=a$$ with a polynomial in powers of $$(x-a)$$ such that the first $$n$$ derivatives of the polynomial match the first $$n$$ derivatives of $$f(x)$$ at $$a$$,
\begin{equation} \label{eq:Taylor}
    f(x) \approx f(a) + (x-a) f'(a) + \frac{(x-a)^2}{2!} f^{\prime\prime}(a) + \cdots +
    \frac{(x-a)^n}{n!} f^{(n)}(a)
\end{equation}
where the inequality comes from ignoring higher-order terms.

A useful way to bound the error associated with ignoring those terms is to integrate the $$n$$th derivative from $$a$$ to $$x$$ $$n$$ times:
\begin{align}
  \int\_a^{x\_{n-1}} f^{(n)} \dd{x\_n} &= f^{(n-1)}(x_{n-1}) - f^{(n-1)}(a) \notag \\\ 
  \int\_a^{x\_{n-2}} \dd{x_{n-1}} \int\_a^{x\_{n-1}} \dd{x\_{n}} f^{(n)}(x_n) &= f^{(n-2)}(x\_{n-2}) - f^{(n-2)}(a) -(x\_{n-2} - a) f^{(n-1)}(a) \notag \\\ 
  \vdots \qquad & \qquad \vdots \notag \\\ 
  &= f(x) - f(a) -(x-a) f'(a) - \frac{(x-a)^2}{2!} f^{\prime\prime}(a) - \cdots - \frac{(x-a)^{n-1}}{(n-1)!} f^{(n-1)}(a)
\end{align}
Rearranging slightly gives
\begin{equation}\label{eq:Taylor2}
  f(x) = \sum\_{i=0}^{n-1} \frac{(x-a)^i}{i!} f^{(i)}(a) + R_n
\end{equation}
where the remainder is the $$n$$-dimensional integral,
\\[
    R_n = \int_a^x \dd{x_1} \cdots \int_a^{x\_{n}} \dd{x\_n} \; f^{(n)}(x_n) = \frac{(x-a)^n}{n!} f^{(n)}(\xi)
\\]
for some value $$a \le \xi \le x$$ by the mean value theorem. Equation (\ref{eq:Taylor2}), with the explicit form of the residual $$R_n$$ is a particularly powerful way of not only estimating functions but also the magnitude of the error associated with a finite series.

## Some Important Taylor Series

Physicists should know the following series cold; they arise very frequently in physics and it is worth your time to learn so well that you don't need to think about them. (Actually, each of these is a **Maclaurin series**, which is a form of Taylor series in which the derivatives are evaluated at $$a = 0$$):

\begin{align}
  e^x &= 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \frac{x^4}{4!} + \cdots &  &-\infty < x <\infty \notag \\\ 
  \sin x &= x - \frac{x^3}{3!} + \frac{x^5}{5!} - \frac{x^7}{7!} + \cdots &  &-\infty < x <\infty \notag \\\ 
  \cos x &= 1 - \frac{x^2}{2!} + \frac{x^4}{4!} - \frac{x^6}{6!} + \cdots &  &-\infty < x <\infty\notag \\\ 
  \sinh x &= x + \frac{x^3}{3!} + \frac{x^5}{5!} + \frac{x^7}{7!} + \cdots &  &-\infty < x <\infty \notag \\\ 
  \cosh x &= 1 + \frac{x^2}{2!} + \frac{x^4}{4!} + \frac{x^6}{6!} + \cdots &  &-\infty < x <\infty\notag \\\ 
  \frac{1}{1-x} &= 1 + x + x^2 + x^3 + x^4 + \cdots & & -1 < x < 1 \notag \\\ 
  \ln(1+x) &= x - \frac{x^2}{2} + \frac{x^3}{3} - \frac{x^4}{4} + \cdots &  &-1 < x \le 1 \notag \\\ 
  (1+x)^n &= 1 + n x + \frac{n(n-1)}{2!} x^2 + \frac{n(n-1)(n-2)}{3!} x^3 + \cdots
  & & -1 < x < 1 \tag{binomial}
\end{align}
Clearly, the radius of convergence of the logarithmic series does not include $$x = -1$$, which generates a divergent harmonic series. For the **binomial series**, the series terminates when $$n$$ is a positive integer and so converges for all $$x$$. When $$n$$ is not a positive integer, the series does not terminate and may not converge.

## Evaluating Limits

Taylor series offer a useful alternative to **l'Hôpital’s rule** for evaluating the limit of the ratio of two functions, $$f(x)$$ and $$g(x)$$, both of which tend to zero as $$x \to x_0$$. As an example, consider
\\[
  L = \lim_{x\to0} \frac{1 - \cos x}{x^2}
\\]
where $$f(x) = 1 - \cos x$$ and $$g(x) = x^2$$, both of which go to zero as $$ x \to 0$$. To evaluate using l'Hôpital’s rule, form $$f'(x)/g'(x)$$:
\\[
    L = \lim_{x\to0} \frac{f'(x)}{g'(x)} = \lim_{x\to0} \frac{\sin x}{2x}
\\]
That's still indeterminate, in the form $$0/0$$, so we can apply l'Hôpital's rule once again to get
\\[
    L = \lim_{x\to0}\frac{f^{\prime\prime}(x)}{g^{\prime\prime}(x)} = \lim_{x\to0}\frac{\cos x}{2} = \frac12
\\]

Alternatively, we can use the Taylor series for $$\cos x$$:
\\[
    L = \lim_{x\to0} \frac{1 - (1 - x^2/2! + x^4/4! - \cdots)}{x^2} = \lim_{x\to0} \frac{1}{2!} - \frac{x^2}{4!} + \cdots
    = \frac12
\\]
No need to compute derivatives (if you already know the Taylor series)! Oftentimes, this approach is much simplier than (successive) "trips to the hospital."

## Manipulating Series

Suppose that you knew a Maclaurin series for a function $$f(x)$$ but you need the series for $$1/f(x)$$, valid for small values of $$x$$. For example, we know the series for $$\cosh x$$ from the above list (or we could derive it ourselves). The hyperbolic secant function, $$\sech x = 1 / \cosh x$$. How could we compute the series for $$\sech x$$, valid for small $$x$$ through terms of order $$x^6$$?

The "easy" way is to go back to the definition in Eq.&nbsp;(\ref{eq:Taylor}) and work out all the derivatives of $$\sech(x)$$. While this is straightforward, in principle, the expressions for the derivatives get more and more complicated as we proceed. [If you don't believe me, try it!]

Here's another option. For small $$x$$, 
\begin{equation}
  \cosh x = 1 + \underbrace{\frac{x^2}{2!} + \frac{x^4}{4!} + \frac{x^6}{6!} + \cdots}_{q}
\end{equation}
where $$q$$ is a "small quantity" as long as $$x$$ isn't too large. So,
\begin{equation}\label{eq:sech1}
  \sech x = \frac{1}{\cosh x} = \frac{1}{1 + q} = (1 + q)^{-1}
\end{equation}
But, the binomial series for $$n = -1$$ is just
\\[
    \frac{1}{1 + q} = 1 - q + q^2 - q^3 + \cdots
\\]
To produce the series for $$\sech x$$ valid for terms through $$x^6$$ just requires us to keep **all** the terms in $$-q + q^2 - q^3$$ through $$x^6$$. We'll work term by term:
\begin{align}
  -q &= -\frac{x^2}{2!} - \frac{x^4}{4!} - \frac{x^6}{6!} - \frac{x^8}{8!} + \O{x^{10}}     \notag \\\ 
  q^2 &= \frac{x^4}{(2!)^2} + 2 \frac{x^2 \; x^4}{2! \; 4!} +
   2 \frac{x^2}{2!} \frac{x^6}{6!} + \left( \frac{x^4}{4!} \right)^2 + \O{x^{10}} \notag \\\ 
   &= \frac{x^4}{4} + \frac{x^6}{4!} + x^8 \left( \frac{1}{6!} + \frac{1}{(4!)^2} \right) + \O{x^{10}} \notag \\\ 
   -q^3 &= -\left(\frac{x^2}{2!} \right)^3 - 3 \left(\frac{x^2}{2!}\right)^2 \frac{x^4}{4!}
   + \O{x^{10}} \notag \\\ 
   q^4 &= \frac{x^8}{16} + \O{x^{10}} \notag
\end{align}

Now, we just need to combine all these terms:
\begin{align}
  \sech x &= 1 - \frac{x^2}{2} +
   x^4 \left( -\frac{1}{4!} + \frac{1}{4} \right) 
   + x^6 \left( -\frac{1}{6!} + \frac{1}{4!} - \frac{1}{8} \right) \notag
   \\\ 
   &\qquad + x^8 \left( -\frac{1}{8!} + \frac{1}{6!} + \frac{1}{(4!)^2} - \frac{1}{32} 
   + \frac{1}{16}
   \right) + \O{x^{10}} \notag \\\ 
   &= 1 - \frac{x^2}{2} + \frac{5 x^4}{24} - \frac{61 x^6}{720} + \frac{277 x^8}{8064} + \O{x^{10}}
\end{align}

<p class="center" markdown="0">
  <img src="figs/sech-expansion.webp" style="width: 400px;" alt="series expansion of sech">
</p>
<p class="icap" markdown="1"><a name="Fig3">Figure 3</a> — Maclaurin series for the hyperbolic cosine obtained by inverting the series for $$\cosh x$$. Each successive curve includes the terms through the order listed in the legend.</p>

See [the page on Euler’s $$\Gamma$$ function](FO-Gamma.md) for an illustration of the power of series expansion as a means of obtaining an analytic expression for the factorial function.

### Exercises

1. Derive a power series expansion through $$x^5$$ for $$\cot x$$ by dividing the series for $$\cos x$$ by the series for $$\sin x$$. Ans: 
\\[
  \cot x = \frac1x - \frac{x}{3} - \frac{x^3}{45} - \frac{2 x^5}{945} + \cdots
\\]
Note that this series includes a negative power of $$x$$, which means it is not a Taylor series. Series that include negative powers are called **Laurent series** and are very common in the theory of functions of a complex variable.

2. The derivative of $$\tan^{-1}x$$ is $$(1+x^2)^{-1}$$. By integrating, find a series expansion for $$\tan^{-1} x$$.

3. One way to compute a series for $$\sin^{-1} x$$ is to start with $$x = \sin y$$. Then $$dx/dy = 


## Problems

1.   The following problem arises in computing a Fresnel diffraction pattern, where
  we need the difference between $$s$$ and $$s_{0}$$ in the following figure:

<p class="center" markdown="0">
  <img src="figs/Fresnel.webp" style="width: 600px;" alt="Geometry for Fresnel diffraction">
</p>
<p class="icap" markdown="1"><a name="Fig4">Figure 4</a> — Geometry of Fresnel diffraction, where $$|x| \ll s_0$$ and the cosine of the angle between $$s_0$$ and $$x$$ is $$x_s / s_0$$.</p>


Compute $$s - s_{0}$$ **to second order in $$x$$**, where the law of cosines gives
\begin{equation}
	s^{2} = s_{0}^{2} + x^{2} - 2 x x_{s}
\end{equation}
  and $$x_{s}$$ is a constant. That is, you may ignore terms proportional to
  $$x^{3}$$ or any higher power of $$x$$.


<!---
## Possible Problems

1. Do certain series converge?
2. Combining absolutely convergent series.
3. Illustrating failure to converge of alternating series?
4. Working out the Taylor series for something
5. Expressing a Gaussian integral in terms of $$\Gamma(x)$$.
6. Multiplying a pair of series to determine unknown coefficients.
-->