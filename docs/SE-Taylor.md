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

You probably know **l'Hôpital’s rule** for evaluating the limit of the ratio of two functions, $$f(x)$$ and $$g(x)$$, both of which tend to zero as $$x \to x_0$$. As an example, consider
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

Ultimately, the justification of l'Hôptial's rule comes from Taylor series, which we can just use directly:
\\[
    L = \lim_{x\to0} \frac{1 - (1 - x^2/2! + x^4/4! - \cdots)}{x^2} = \lim_{x\to0} \frac{1}{2!} - \frac{x^2}{4!} + \cdots
    = \frac12
\\]
No need to compute derivatives (if you already know the Taylor series)! Oftentimes, this approach is much simplier than (successive) "trips to the hospital."

[Next: Manipulating Series](SE-Manipulate.md)
