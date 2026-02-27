{:menu FO}

# More Examples of Contour Integration

* toc
{:toc}

## A Second-Order Pole

Consider the integral
\\[
    I = \int_{-\infty}^{\infty} \frac{\sin^2 x}{x^2} \dd{x}
\\]
whose integrand is shown in Fig.~1. Clearly, it is well-behaved at the origin, and finite, since it dies nicely for large $$|x|$$. Can we use contour integration to evaluate it?

<p class="figure" markdown="0">
  <img src="figs/FO-CE1.webp" style="width: 400px;" alt="sinc^2 function">
</p>
<p class="icap" markdown="1"><a name="Fig1">Figure 1</a> — A graph of $$\sin^2x / x^2$$.</p>

The first step is to express sine in terms of complex exponentials,
\\[
    I = \int_{-\infty}^{\infty} \left(\frac{e^{iz} - e^{-iz}}{2iz} \right)^2
    \dd{z} =
    \int_{-\infty}^{\infty} \frac{e^{2iz} - 2 + e^{-2iz}}{-4z^2}\dd{z}
\\]
The first exponential will be well-behaved in the upper half-plane (UHP), whereas the second one will be well-behaved in the LHP. We're going to have to break the integrand up to allow us to generate closed contours. So, we have
\\[
    I = -\frac14 \int_{-\infty}^{\infty}
    \frac{e^{2iz}-1}{z^2} \dd{z}
    -\frac14 \int_{-\infty}^{\infty}
    \frac{e^{-2iz}-1}{z^2} \dd{z}
\\]
