{:menu FO}


# Euler's Gamma Function

* toc
{:toc}


You are quite familiar with factorials,
\\[
    n! = n \times (n-1) \times \cdot \times 2 \times 1
\\]
with the understanding that $$0! = 1$$. The gamma function generalizes the factorial function to nonintegral values. It is defined by
\\[
    \Gamma(n+1) = \int_0^\infty x^n e^{-x} \dd{x}
\\]
where the extra 1 in the argument is courtesy of Legendre. To see that $$\Gamma(n+1)$$ corresponds to the factorial function, integrate by parts:
\\[
    \Gamma(n+1) =  \underbrace{\left. n x^{n-1} e^{-x} \right|\_0^\infty}\_{\text{vanishes}} + \int_0^\infty n x^{n-1} e^{-x}\dd{x} = n \Gamma(n)
\\]
or
\begin{equation}\label{eq:recurrence}
  \Gamma(n+1) = n \Gamma(n)
\end{equation}

When $$n = 1$$, we have a straightforward integral to do
\\[
    \Gamma(1) = \int_0^\infty x^0 e^{-x} \dd{x} = \left. -e^{-x} \right|\_0^\infty = 1
\\]
Hence, the recursion relation $$\Gamma(n+1) = n \Gamma(n)$$ along with the termination condition $$\Gamma(1) = 1$$ proves that $$\Gamma(n+1) = n!$$ for nonnegative integer $$n$$.

What about when $$n$$ is non-integral? For instance, what about $$n = -\frac12$$? That is, can we evaluate
\\[
    I = \int_0^\infty \frac{1}{\sqrt{t}} e^{-t} \dd{t}
\\]
Let $$x = \sqrt{t}$$ or $$x^2 = t$$, so that $$\dd{t} = 2 x \dd{x} $$, giving
\\[
    I = \int_0^\infty \frac1x e^{-x^2} 2x \dd{x}  = 2\int_0^\infty e^{-x^2}\dd{x} = \int_{-\infty}^{\infty} e^{-x^2}\dd{x}
\\]
While it may not look like we are any closer to an evaluation, it is undeniably true that squaring this expression yields
\\[
    I^2 = \int_{-\infty}^\infty \dd{x} \int_{-\infty}^\infty \dd{y} \, e^{-x^2} e^{-y^2} =
    \int_{-\infty}^\infty \dd{x} \int_{-\infty}^\infty \dd{y} \; e^{-(x^2+y^2)}
\\]
since both $$x$$ and $$y$$ are dummy variables of integration. On the other hand, we can read this expression as the integral over the $$xy$$ plane of the integrand $$e^{-x^2-y^2} = e^{-r^2}$$, where $$r$$ is the distance from the origin. Rather than integrating in cartesians, we can use polar coordinates:
\\[
    I^2 = \int_0^{2\pi} \int_0^\infty e^{-r^2} \, r \dd{r} \dd{\theta}
\\]
Making the $$u$$ substitution $$u = r^2$$, so that $$\dd{u} = 2 r \dd{r}$$, we can rewrite this double integral as
\\[
    I^2 = \int_0^{2\pi} \int_0^\infty e^{-u}  \frac{\dd{u}}{2} \dd{\theta} = \pi
\\]
Therefore,
\\[
    I = \Gamma\qty(\frac12) =  \int_{-\infty}^\infty e^{-x^2}\dd{x} = \sqrt{\pi}
\\]
We can then use the recurrence relation of Eq. (\ref{eq:recurrence}) to deduce that
\begin{align}
    \Gamma\qty(\frac32) &= \frac12 \Gamma\qty(\frac12) = \frac{\sqrt{\pi}}{2} \notag \\\ 
    \Gamma\qty(\frac52) &= \frac32 \Gamma\qty(\frac32) = \frac{3\sqrt{\pi}}{4} \notag
\end{align}
and in general
\\[
    \Gamma\qty(n+\frac12) = \frac{2n-1}{2} \times \frac{2n-3}{2} \times \cdots \frac{1}{2} \Gamma\qty(\frac12)
    = \frac{(2n-1)!!}{2^n} \sqrt{\pi}
\\]
where the double factorial is defined by
\\[
    n!! = n \times (n-2) \times \cdots \times \begin{cases} 1 & n\text{ odd} \\\ 
    2 & n\text{ even}
    \end{cases}
\\]

<p class="center" markdown="0">
  <img src="figs/gamma.webp" style="width: 500px;">
</p>
<p class="mycap" markdown="1">The gamma function $$\Gamma(x)$$ for small arguments $$x$$. For large values of $$x$$, $$\Gamma(x) = (x-1)!$$.</p>

The figure was generated with the following Python code:

~~~~ python
import matplotlib.pyplot as plt
from scipy.special import gamma

f,a = plt.subplots()
x = np.linspace(0.5, 4, 100)
a.plot(x, gamma(x))
a.set_xlabel("$x$")
a.set_ylabel(r"$\Gamma(x)$");
~~~~

## Stirling's Approximation

Factorials grow extremely rapidly with their argument; it could be handy to have an approximate expression. It might be easier to estimate $$\ln n!$$, though, since the logarithm converts all the multiplications to addition:
\\[
    \ln n! = \ln 1 + \ln 2 + \cdots + \ln n
\\]

<p class="center" markdown="0">
  <img src="figs/baby-Stirling.webp" style="width: 400px;" alt="The logarithm of n!">
</p>
<p class="icap" markdown="1"><a name="Fig1">Figure 1</a> — A way to estimate $$\ln x!$$ would be to compute the area under the red curve, although that sure looks like an overestimate, since there is area outside the blue bars. By contrast, the area under the green curve would be an underestimate, since it is entirely contained in the bars.</p>

The area under the red curve would be
\\[
    \ln n!\_{\text{red}} = \int\_{1}^{n+1} \ln x \dd{x} = x\ln x - x \bigg|\_1^{n+1} = (n+1) \ln (n+1) - n - 1
\\]
The upper limit on the integral is $$n+1$$ because the bar for $$\ln n$$ starts at $$n$$ and goes to $$n+1$$. The area under the green curve would be
\\[
    \ln n!\_{\text{green}} = \int\_{2}^{n+1} \ln (x-1) \dd{x} = \int\_1^{n} \ln x' \dd{x'} = x'\ln x' - x' \bigg|\_1^{n} = 
    n \ln n - n
\\]
The true value lies above green but below red. So, crudely, $$\ln n! \approx n \ln n - n$$ and $$n! \approx n^n e^{-n}$$, although that's going to be a modest underestimate. As a spot check, we can evaluate $$6! = 720$$:
\\[
    6^6 e^{-6} = 115.65
\\]
Wow, that's not very good, is it? Well, the red estimate would be $$7^7 e^{-7} = 751$$, so at least the upper bound seems pretty reasonable.

## A Continuum Approach

We know from above that $$\Gamma(n+1) = n!$$ for nonnegative integers $$n$$. That is,
\\[
    n! = \int_0^{\infty} x^n e^{-x} \dd{x}
\\]
The integrand is the product of a rapidly increasing function of $$x$$ (at large $$n$$) and a rapidly decreasing function of $$x$$. There's a peak somewhere. Maybe we could develop an approximation by expanding about that peak. 

<p class="center" markdown="0">
  <img src="figs/gamma-integrand.webp" style="width: 400px;" alt="The integrand of the gamma function">
</p>
<p class="icap" markdown="1"><a name="Fig2">Figure 2</a> — The integrand of $$\Gamma(x)$$, shown here for $$n = 6$$. It is peaked in the vicinity of $$x = n$$.</p>

Actually, it will be smoother if we expand the logarithm of the integrand around the peak, and then exponentiate our series expansion. So, the steps are:

1. Let $$ y = \ln(x^n e^-x) $$ and find where $$y$$ has a maximum.
2. Expand $$y$$ around its maximum in a Taylor series.
3. Integrate $$\exp(\text{our approximate series})$$ to get an approximation to $$n!$$.

### Step 1: Find the Maximum

\begin{equation}
  y = n \ln x - x  \qqtext{so} y' = \frac{n}{x} - 1
\end{equation}
Evidently, the peak at $$y' = 0$$ occurs when $$x = n$$, so we will look to expand about that point.

### Step 2: Expand $$y$$ in a Taylor Series

\begin{align}
  i &= 2 & \qquad y'' &=  -\frac{n}{x^2} &\qquad y'' (n) &= -\frac{1}{n} \notag \\\ 
  i &= 3 & \qquad y''' &=  \frac{2n}{x^3} &\qquad y''' (n) &= \frac{2}{n^2} \notag \\\ 
  i &= 4 & \qquad y^{\text{iv}} &=  -\frac{3! n}{x^4} &\qquad y^{\text{iv}} (n) &= \frac{3!}{n^3} \notag \\\ 
  i &= 5 & \qquad y^{\text{v}} &=  \frac{4! n}{x^5} &\qquad y^{\text{v}} (n) &= \frac{4!}{n^4} \notag
  \end{align}

I think I see the pattern here. So
\begin{equation}\label{eq:Taylor}
  y = n \ln n - n - \frac{(x-n)^2}{2!\;n} + \frac{2!(x-n)^3}{3!\;n^2} - \frac{3!(x-n)^4}{4!\; n^3}+ \cdots
\end{equation}
We can simplify the notation by letting $$\xi = x-n$$:
\begin{equation}\label{eq:ybetter}
  y = n \ln n - n - \frac{\xi^2}{2n} + \frac{\xi^3}{3n^2} - \frac{\xi^4}{4n^3} + \cdots
\end{equation}

### Step 3: A First Pass

To get our feet wet, let's just include the first term in this series with $$\xi$$ dependence. Then we have
\begin{align}
  n! &\approx \int_{-n}^\infty \exp\left[ n\ln n - n - \frac{\xi^2}{2n} \right] \dd{\xi}  \notag
  &= n^n e^{-n} \int_{-n}^\infty e^{-\alpha \xi^2} \dd{\xi} \notag
\end{align}
where I have defined $$\alpha \equiv 1/2n$$. If we could let the lower limit go off to $$-\infty$$, we would know that the integral was $$\sqrt{\pi/\alpha} = \sqrt{2 \pi n}$$. Looking at Fig.&nbsp;2, it might seem like a reasonable approximation; the integrand seems really small there. Our new approximation to $$n!$$ is
\begin{equation}\label{eq:nfact2}
  n! \approx \sqrt{2 \pi n} \; n^n e^{-n}
\end{equation}
When $$n = 6$$, this approximation gives 710.1, which is a heck of a lot closer to the true value of 720 than our first approximation. 

<p class="center" markdown="0">
  <img src="figs/gamma-first-pass.webp" style="width: 400px;" alt="First term in the Stirling approximation">
</p>
<p class="icap" markdown="1"><a name="Fig3">Figure 3</a> — The integrand of $$\Gamma(7) = 6!$$ (black curve) and the approximate integrand from Eq.&nbsp;(\ref{eq:ybetter}) when we include only the term quadratic in $$\xi = x-n$$.</p>

Looking at the approximate integrand for $$n = 6$$ in Fig.&nbsp;3, it seems clear that we are overcounting area to the left of the peak and undercounting to its right. It seems likely that for larger values of $$n$$ we are probably going to be doing better. Let's make a quick check: 

<div class="center-div">
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>$$n$$</th>
      <th>$$n!$$</th>
      <th>$$n^n e^{-n} / n!$$</th>
      <th>$$\sqrt{2\pi n} \, n^n \, e^{-n} /n!$$</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>1</td>
      <td>0.367879</td>
      <td>0.922137</td>
    </tr>
    <tr>
      <td>2</td>
      <td>2</td>
      <td>0.270671</td>
      <td>0.959502</td>
    </tr>
    <tr>
      <td>3</td>
      <td>6</td>
      <td>0.224042</td>
      <td>0.972702</td>
    </tr>
    <tr>
      <td>4</td>
      <td>24</td>
      <td>0.195367</td>
      <td>0.979424</td>
    </tr>
    <tr>
      <td>5</td>
      <td>120</td>
      <td>0.175467</td>
      <td>0.983493</td>
    </tr>
    <tr>
      <td>6</td>
      <td>720</td>
      <td>0.160623</td>
      <td>0.986220</td>
    </tr>
    <tr>
      <td>7</td>
      <td>5040</td>
      <td>0.149003</td>
      <td>0.988174</td>
    </tr>
    <tr>
      <td>8</td>
      <td>40320</td>
      <td>0.139587</td>
      <td>0.989643</td>
    </tr>
    <tr>
      <td>9</td>
      <td>362880</td>
      <td>0.131756</td>
      <td>0.990787</td>
    </tr>
    <tr>
      <td>10</td>
      <td>3628800</td>
      <td>0.125110</td>
      <td>0.991704</td>
    </tr>
  </tbody>
</table>
</div>

So, that hunch seems to be right; by $$n = 10$$, our approximation that includes the Gaussian integral is closer than 1% to the true value.

### Step 4: Series Corrections

