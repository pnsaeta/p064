{:menu FO}
{::comment}menu-start{:/comment}

<div class="dropdown">
<label id="main-menu"><img id="master" src="figs/master.webp"></label>
<div class="dropdown-content">
<ul>
<li><a href="SW-Installation.html">Software Installation</a></li>
<li><a href="LA-LinearAlgebra.html">Linear Algebra</a></li>
<li><a href="FO-Intro.html">Fourier Series and Transforms</a></li>
<li><a href="ST-Random.html">Stochastic Processes</a></li>
<li><a href="DE-DE1.html">Differential Equations</a></li>
<li><a href="PD-PD1.html">Partial Differential Equations</a></li>
<li><a href="PR-Project.html">Projects</a></li>
</ul>
</div>
</div>
<div class="dropdown hamburger">
<label id="hamburger-menu"><img id="hamburger" src="figs/hamburger.webp"></label>
<div class="dropdown-content">
<ul>
<li><a href="FO-Intro.html">Complex Numbers and All Things Fourier</a></li>
<li><a href="FO-ComplexVariables.html">Complex Variables</a></li>
<li><a href="FO-Series.html">Series</a></li>
<li><a href="FO-FourierSeries.html">Fourier Series</a></li>
<li><a href="FO-FourierTransforms.html">Fourier Transforms</a></li>
<li><a href="FO-Delta.html">The Dirac Delta Function</a></li>
<li><a href="FO-Numerical-FFT.html">Numerical Fourier Transforms</a></li>
</ul>
</div>
</div>

{::comment}menu-end{:/comment}


# The Dirac Delta Function

We seek to prove that
\begin{equation}\label{eq:FourierDelta}
  \boxed{\delta(x) = \frac{1}{2\pi} \int_{-\infty}^{\infty} e^{ikx} \dd{k}}
\end{equation}

Well, suppose that $$x \ne 0$$. Then the integrand is a phase that spins endlessly around the clock dial. Every point on the unit circle gets passed countless times; no point is more favored than any other, so the average is zero. On the other hand, if $$x = 0$$, then every phase is zero and we are adding up 1 over the infinite range, which sure seems like a recipe for infinity. So, at least *qualitatively*, this expression seems reasonable.

The quintessential behavior of a delta function is revealed by integrating over it. To confirm that
\\[
    \frac{1}{2\pi} \int_{-\infty}^{\infty} e^{ik x} \dd{k} = \delta(x)
\\]
let's integrate from $$x_1$$ to $$x_2$$. If these two points straddle zero, we should get something. If they don't, we should get zero.
\begin{equation}\label{eq:a}
    a = \int_{x_1}^{x_2}  \dd{x} \frac{1}{2\pi}
    \int_{-\infty}^{\infty} e^{ikx} \dd{k}
    = \frac{1}{2\pi} \int_{-\infty}^{\infty} \dd{k}
    \int_{x_1}^{x_2} e^{ikx} \dd{x}
    = \frac{1}{2\pi} \int_{-\infty}^{\infty}  \dd{k}
    \frac{e^{ikx_2} - e^{ikx_1}}{ik}
\end{equation}
This is two integrals of the form
\\[
    b(x_n) = \frac{1}{2\pi i} \int_{-\infty}^{\infty} \frac{e^{ikx_n}}{k} \dd{k}
\\]
Let's see if we can evaluate this integral using contour integration on the complex plane. That is, we want to find a closed contour around which we can integrate
\\[
   I = \frac{1}{2\pi i} \oint \frac{e^{i x_n z}}{z} \dd{z}
\\]
so that the path includes the integral we want (going from $$-\infty$$ to $$\infty$$ along the real axis) and then finding a way to close the contour that doesn't add anything to the integral.

Suppose that $$x_n > 0$$. Then if we close along a semicircle at $$ R = \infty $$ in the upper half-plane (UHP), along that path we have $$z = R e^{i \theta}$$ so that $$\dd{z} = iR e^{i \theta} \dd{\theta}$$
\\[
    I = \frac{1}{2\pi i} \int_0^{\pi} \frac{e^{i x_n R (\cos\theta + i\sin\theta)}}{R e^{i\theta}} i R e^{i\theta}\dd{\theta} = \frac{1}{2\pi} \int_{0}^{\pi} e^{ix_nR\cos\theta}
    e^{-x_n R \sin\theta} \dd{\theta}
\\]
In the UHP, the second exponential goes strongly to zero, while the first exponential oscillates at a frequency that diverges. Therefore, $$I \to 0$$ and by closing along the semicircular path at $$R \to \infty$$ in the UHP, we add no additional contribution to the integral.

<p class="center" markdown="0">
  <img src="figs/UHP.webp" style="width: 300px;">
</p>
<p class="mycap" markdown="1">Contour closing in the upper half-plane appropriate when $$x_n > 0$$.</p>

We now need to evaluate $$I$$ along the illustrated path. The integrand has a simple pole at $$z = 0$$ which lies exactly along the path. We can either deviate the path on a tiny semicircular path passing underneath the origin, which puts the pole inside the path, or deviate on a tiny semicircle above the origin, which will exclude the pole from the path. I'll take the former choice, as illustrated in the following figure.

<p class="center" markdown="0">
  <img src="figs/CauchyPValue.webp" style="width: 300px;">
</p>
<p class="mycap" markdown="1"></p>

 Along that tiny semicircle, $$z = \epsilon e^{i\theta}$$ for $$\pi \le \theta \le 2\pi$$. The contribution to the path integral along this tiny portion of path is thus
\\[
    I_{sc} = \int_{\pi}^{2\pi} \frac{e^{ix_n \epsilon e^{i\theta}}}{\epsilon e^{i\theta}} i\epsilon e^{i\theta} \dd{\theta} = i \int_\pi^{2\pi} e^{i x_n \epsilon e^{i\theta}} \dd{\theta} = i\pi
\\]
as $$\epsilon \to 0$$. By distorting the path, we have added $$i\pi$$ to the value of the integral, so we need to subtract if from the result. Since the pole now lies within the contour, by the residue theorem, the value of the adjusted integral is
\\[
    I = \frac{1}{2\pi i}\times \qty(2\pi i a_{-1} - i\pi) = \frac{1}{2}
\\]
since $$a_{-1} = e^0 = 1$$. Or, translating back to $$b(x_n)$$, we have
\\[
    b(x_n) = \frac12 \qqtext{if $$x_n > 0$$}
\\]

If, on the other hand, $$x_n < 0$$, we must close in the lower half-plane (LHP). By an argument analogous to the one given just now—and noting that when we close in the LHP, we traverse the contour in the clockwise (negative) direction—we find that 
\\[
    b(x_n) = -\frac12 \qqtext{if $$x_n < 0$$}
\\]
But this is *exactly* what we need. If $$x_1$$ and $$x_2$$ have the same sign, then they integrate to give the same value (either $$\frac12$$ or $$-\frac12$$) and cancel one another in Eq. (\ref{eq:a}). If they straddle zero and $$x_2 > x_1$$ then the integral gives $$\frac12 - (-\frac12) = 1$$, as we expect for a $$\delta$$ function: integrating over where it turns on should give unity. If $$x_1$$ and $$x_2$$ straddle in the opposite order, then we get $$-1$$, again as we expect.