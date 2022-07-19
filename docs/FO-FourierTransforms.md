{:menu FO}
{::comment}menu-start{:/comment}

<div class="dropdown">
<label id="hamburger-menu"><img id="hamburger" src="figs/hamburger.png"></label>
<div class="dropdown-content">
<ul>
<li><a href="FO-Intro.html">Introduction to Fourier Series and Transforms</a></li>
<li><a href="FO-ComplexVariables.html">Complex Variables</a></li>
<li><a href="FO-Series.html">Series</a></li>
<li><a href="FO-FourierSeries.html">Fourier Series</a></li>
<li><a href="FO-FourierTransforms.html">Fourier Transforms</a></li>
</ul>
</div>
</div>

{::comment}menu-end{:/comment}


# Fourier Transforms

* toc
{:toc}

[Back to the top](index.md)

## Definition

In Engineering 79 you got some practice using **Laplace transforms** to convert differential equations into algebraic equations. Recall that the Laplace transform of a function $$f(t)$$ is given by
\\[
  F(s) = \int_{0}^{\infty} f(t) e^{-st}\dd{t}
\\]
After performing various algebraic manipulations in "Laplaceland", you either recognized the resulting function as the Laplace transform of a known function of time, or you used a table of transforms to perform the inversion.

A **Fourier transform** is similar in some respects, but has a more symmetric structure for going between time and frequency space. It may be defined by
\begin{align}
  \tilde{f}(\omega) &= \int_{-\infty}^\infty f(t) e^{-i\omega t} \dd{t}  \label{eq:FT1} \\\ 
  f(t) &= \frac{1}{2\pi} \int_{-\infty}^\infty  \tilde{f}(\omega) e^{i\omega t}\dd{\omega} \label{eq:FT2}
\end{align}
I say "may be" because different authors use different conventions on how to distribute the factor of $$1/2\pi$$ between the two expressions. For example, it is common in quantum mechanics to put a factor of $$1/\sqrt{2\pi}$$ in front of each integral.

Before attempting to justify these two expressions, let's play around a bit. Suppose, for instance, that $$f(t) = \cos(\Omega t)$$, a cosine wave at angular frequency $$\Omega$$. If we substitute into Eq. (\ref{eq:FT2}), we get
\\[
    \cos\Omega t = \frac{e^{i\Omega t} + e^{-i\Omega t}}{2} 
    = \frac{1}{2\pi} \int_{-\infty}^{\infty}
    \tilde{f}(\omega) e^{i\omega t} \dd{\omega}
\\]
On the right-hand side, we integrate over all frequencies, but on the left-hand side we have a sum of just two frequencies, $$\Omega$$ and $$-\Omega$$. Evidently, $$\tilde{f}(\omega)$$ must be zero when $$\omega \ne \pm \Omega$$. On the other hand, it must really blow up when $$\omega = \pm \Omega$$ in just the right way so that integrating over the spike gives the finite results on the left. That is, it must be
\\[
    \tilde{f}(\omega) = \pi \delta(\omega - \Omega) + \pi \delta (\omega + \Omega)
\\]
where the **Dirac delta function** is the limiting case of a peak with unit area as its width shrinks to zero. 

## Dirac Delta Function

One way to represent it would be a skinny rectangle:
\\[
    \delta (x - x_0) = \lim_{\epsilon \to 0} 
    \begin{cases} 
      \frac{1}{\epsilon} & |x-x_0| < \epsilon/2 \\\ 
      0 & \text{otherwise}
    \end{cases}
\\]
Another would be a normalized Gaussian peak, 
\\[
    G(x) = \frac{1}{\sqrt{2\pi \sigma^2}} \exp\qty[\frac{(x-x_0)^2}{2\sigma^2}]
\\]
whose width tends to zero
\\[
    \delta (x - x_0) = \lim_{\sigma \to 0} 
    \frac{1}{\sqrt{2\pi \sigma^2}} \exp\qty[\frac{(x-x_0)^2}{2\sigma^2}]
\\]
For finite $$\sigma$$, the peak has unit area and as $$\sigma \to 0$$ the region over which the function differs appreciably from zero shrinks to zero.

To see that Eqs. (\ref{eq:FT1}) and (\ref{eq:FT2}) are consistent with one another, we could substitute Eq. (\ref{eq:FT1}) into Eq. (\ref{eq:FT2}), taking care to a different (dummy) variable of integration for Eq. (\ref{eq:FT1}):
\\[
    f(t) \overset{?}{=} \frac{1}{2\pi} \int_{-\infty}^{\infty}  \dd{\omega} e^{i\omega t}
    \int_{-\infty}^{\infty}  \dd{t'} f(t') e^{-i\omega t'}
\\]
Assuming that $$f$$ dies off adequately at infinity, we may exchange the order of these two integrations:
\\[
    f(t) \overset{?}{=} \int_{-\infty}^{\infty} \dd{t'}
     f(t')  \times 
     \underbrace{\frac{1}{2\pi} \int_{-\infty}^{\infty} \dd{\omega} e^{i\omega (t-t')}}_{\delta(t-t')}
\\]




+ Definition and connection to Fourier series
+ Example transform pairs
+ Connection to Laplace from STEMs?
+ Inversion?
+ Convolutions
+ Correlations
+ Power spectra
