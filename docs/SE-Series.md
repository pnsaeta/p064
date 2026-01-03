{:menu SE}

# Series

* toc
{:toc}

An infinite series is an infinite sum,
\begin{equation}\label{eq:infseries}
  S = \sum_{n=1}^{\infty} a_n = \lim_{N\to\infty} \sum_{n=1}^N a_n
\end{equation}
that is the limit of partial sums having a finite number of terms. For the limit to exist, the magnitude of the terms $$a_n$$ must go to zero as $$n\to\infty$$. However, while this is a necessary condition it is not sufficient. Series are among the most important mathematical tools in the physicist's toolbox. You are no doubt already familiar with Taylor series; for problems that are difficult to solve exactly, we can often satisfactory approximations by truncating a Taylor series. For example, the equation of a simple pendulum is
\\[
    \dv[2]{\theta}{t} + \frac{g}{L} \sin\theta = 0
\\]
It is a **nonlinear** differential equation because the variable $$\theta(t)$$ appears as a nonlinear function. That is
\\[
    \sin \theta = \theta - \frac{\theta^3}{3!} + \frac{\theta^5}{5!} - \cdots
\\]
includes terms with higher powers of $$\theta$$ than the first. However, if we ignore all terms but the first in the Taylor series for $$\sin\theta$$, we obtain
\\[
    \dv[2]{\theta}{t} + \frac{g}{L} \theta = 0
\\]
which is the equation of a simple harmonic oscillator and has a solution we can readily compute.

Key issues we need to understand include:

1. Does an infinite series converge?
2. Can we find a closed-form expression for the infinite sum?
3. Can a series be manipulated term by term?

## Examples

### Harmonic Series

The **harmonic series**,
\\[
    H = \sum_{n=1}^{\infty} \frac1n = 1 + \frac12 + \frac13 + \cdots
\\]
does not converge, even though its terms tend to zero as $$n \to \infty$$. Its divergence is logarithmic (i.e., weak), as illustrated in the following figure

<p class="center" markdown="0">
  <img src="figs/harmonic.webp" style="width: 400px;" alt="Harmonic series">
</p>
<p class="icap" markdown="1"><a name="Fig1">Figure 1 </a> — The harmonic series is represented by the area shaded blue of the bars of height $$1$$, $$\frac12$$, $$\frac13$$, etc. The area of the bars is greater than the area under the curve $$1/x$$ (shown in red), since the curve is everywhere contained within a bar. Since $$\int_1^x \frac1{x'}\dd{x'} = \ln x$$, which slowly diverges as $$x\to\infty$$, the harmonic series diverges even though its individual terms tend to zero.</p>


### Geometric Series

Successive terms of a **geometric series** form a fixed ratio $$r$$:
\\[
    S_N = a_0(1 + r + r^2 + \cdots r^N) = \sum_{n=0}^N a_0 r^n
\\]
There is a nifty trick for summing a (finite) geometric series. Consider $$r S_N$$:
\begin{align}
    S\_N &= a\_0 (1 + r + r^2 + \cdots + r^N) \\\ 
    r S\_N &= a\_0(\hphantom{1 + } \;\, r + r^2 + \cdots + r^N + r^{N+1})
\end{align}
If we now subtract the second line from the first, we get
\begin{equation}
  \label{eq:geo}
  S_N (1-r) = a_0 (1 - r^{N+1}) \qquad\text{so}\qquad \boxed{ S_N = a_0 \left( \frac{1 - r^{N+1}}{1 - r} \right) }
\end{equation}

The series converges to $$S_{\infty} = \frac{a_0}{1-r}$$ as $$N\to\infty$$, provided that
$$|r| < 1$$ (so that the numerator of the fraction goes to 1). Sometimes it is convenient to symmetrize this expression by factoring out $$r^{N/2}$$, which allows you to express the fraction in terms of the ratio between hyperbolic sine functions.

## Tests of Convergence

It is often necessary to know whether an infinite series converges to a finite value. Some of the useful tests to answer this question are:

1. **Comparison tests**: by comparing one series of unknown convergence term-by-term to a series of known convergence properties, it may be possible to deduce the convergence of the first series. For instance, if the series of terms $$\sum_n a_n$$ is known to converge and $$b_n < a_n$$ for all $$n$$, then $$\sum_n b_n$$ converges.
2. **Cauchy Root Test**: if $$(a_n)^{1/n} \le r < 1$$ for all terms $$n \ge N$$, with $$r$$ independent of $$n$$, then $$\sum_n a_n$$ converges. This test is a comparison to the convergence of a geometric series.
3. **Ratio test**: the convergence of a series may be determined from the limit of the ratio of successive terms:
\\[
    \lim_{n\to\infty} \frac{a_{n+1}}{a_n} \begin{cases}
    < 1 &\quad \text{convergence} \\\ 
    > 1 &\quad \text{divergence} \\\ 
    = 1 &\quad \text{indeterminate}
    \end{cases}
\\]
4. **Integral test**: The caption to Fig. 1 above illustrates using an integral test 

### Exercises

1. Use numpy to confirm Eq. \ref{eq:geo} for $$r = 0.99$$ and $$N=100$$.

1. Does the series $$\displaystyle \sum_{n=2}^{\infty} \frac{1}{n \ln n}$$ converge?

2. (a) Show that the series $$\displaystyle \sum_{n=2}^\infty \frac{1}{n(\ln n)^2}$$ converges. (b) Use numpy to sum the terms through $$n = 100,000$$. You should get 2.022 883 9. (c) Use an integral to obtain the sum of the infinite series to six significant figures.

3. Does the series $$\displaystyle \sum_{n=1}^{\infty} \frac{1}{n(n+1)}$$ converge? If it does, can you sum it?

## Riemann Zeta Function

The **Riemann zeta** function is defined by
\begin{equation}\label{eq:zeta}
  \zeta(\nu) = \sum_{n=1}^\infty \frac1{n^{\nu}}
\end{equation}
If $$\nu=1$$, this series becomes the harmonic series, which we know to be divergent. For $$\nu < 1$$ it diverges more rapidly, but for $$\nu > 1$$ we can use an integral test to check convergence:
\\[
    \zeta(\nu) = \sum_{n=1}^\infty \frac1{n^{\nu}} 
    < 1 + \int_2^{\infty} (x-1)^{-\nu} \dd{x}
    = 1 + \left.\frac{(x-1)^{1-\nu}}{1-\nu}\right|_{x=2}^{\infty} = 1 + \frac{1}{\nu-1} = \frac{\nu}{\nu-1} < \infty
    \qquad\text{when } \nu > 1
\\]

<p class="center" markdown="0">
  <img src="figs/zeta.webp" style="width: 400px;" alt="Riemann zeta function">
</p>
<p class="icap" markdown="1"><a name="Fig2">Figure 2 </a> — The Riemann zeta function for $$\nu = 1.1$$. The red and green curves clearly bound the area of the blue bars, which represents the Riemann $$\zeta$$&nbsp; for $$\nu = 1.1$$ (note the logarithmic vertical scale).</p>

The Riemann zeta function pops up occasionally in physics, including the theory of blackbody radiation and the determination of the Stefan-Boltzmann constant, $$\sigma$$, which relates the power per unit area radiated by an ideal blackbody at temperature $$T$$:
\begin{equation}\label{eq:Stefan-Boltzmann}
  p = \sigma T^4 \qquad\text{where}\qquad
  \sigma = \frac{6 \zeta(4) k\_{\mathrm{B}}^4}{\pi^2 c^2 \hbar^3}
  = \frac{2 \pi^5 k\_{\mathrm{B}}^4}{15 c^2 h^3}
  \approx 5.67 \times 10^{-8}\,\mathrm{W \cdot m^{-2} \cdot K^{-4}}
\end{equation}


## Alternating Series

If successive terms in a series alternate sign, and if the magnitude of the terms goes to zero as $$n\to\infty$$, then the series converges. An infinite series is **absolutely** convergent if the sum of the absolute value of its terms converges. If the series converges, but it is not absolutely convergent, it is called **conditionally** convergent.

Properties of absolutely convergent series:

+ the series sum is independent of the order in which one adds the terms
+ two absolutely convergent series may be added, subtracted, or multiplied termwise to yield another absolutely convergent series
+ the product of two absolutely convergent series converges to the product of the individual series

Note that **none of these claims** can be made for conditionally convergent series.

Next: [Taylor Series](SE-Taylor.md)