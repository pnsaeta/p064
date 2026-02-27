{:menu FO}

# More Examples of Contour Integration

* toc
{:toc}

## A Fake Second-Order Pole

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
    I = \int_{-\infty}^{\infty}
    \frac{1-e^{2iz}}{4z^2} \dd{z}
    + \int_{-\infty}^{\infty}
     \frac{1-e^{-2iz}}{4z^2} \dd{z}
\\]
Both integrands have poles at $$z = 0$$ which lie directly on the path of integration, so will only earn half the usual $$2\pi i a_{-1}$$. However, each is a first-order pole, since the numerators are proportional to $$z$$ for $$z \to 0$$. Closing the contour for the first integral in a semicircle at $$R \to \infty$$ in the UHP, it is straightforward to show that this addition adds nothing the integral, so its value will be $$\pi i a_{-1}$$ as $$z \to 0$$. The residue of the first integrand is
\\[
    a_{-1}^+ = \lim_{z\to 0} z \frac{1 - (1 + 2iz + (2iz)^2/2! + \cdots)}{4z^2}
    = \lim_{z\to 0} - \frac{2iz^2}{4z^2} = \frac{1}{2i}
\\]
and by similar argument, the residue of the second integrand is $$a_{-1}^- = -\frac{1}{2i}$$.
So, it might seem that they wipe each other out.

However, since we have to close the contour for the second integral in the LHP, we traverse the contour in the negative direction, so we get $$-\pi i$$ times that residue, which means they reinforce each other. Hence,
\\[
    I = \pi i \left(\frac{1}{2i} \right) - \pi \left(-\frac{1}{2i} \right) = \pi
\\]

## Summing a series

The Riemann zeta function is $$\zeta(n) = \sum_{j=1}^\infty j^{-n}$$.
