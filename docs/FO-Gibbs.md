{:menu FO}


# The Gibbs Phenomenon

* toc
{:toc}

We saw on [the previous page](FO-FourierSeries.md) that the Fourier series for a square wave overshot the mark at the point of discontinuity at $$t = 0$$ where the square wave jumps from $$-1$$ to $$1$$, as illustrated in Fig.&nbsp;1.

<p class="center" markdown="0">
  <img src="figs/square-near-zero.webp" style="width: 500px;" alt="Fourier series for a square wave near a discontinuity">
</p>
<p class="icap" markdown="1"><a name="Fig1">Figure 1</a> — At the point of discontinuity at $$t = 0$$, the series is clearly converging to the midpoint between the limit values on either side. As the number of terms increases, the transition from $$-1$$ to $$1$$ grows narrower, but the **Gibbs** overshoot phenomenon persists.</p>

Is there a way to quantify this overshoot?
We found that the series representing the square wave is
\begin{equation}\label{eq:squarewave}
    f(t) = \frac{4}{\pi} \sum\_{n\text{ odd}}^\infty \frac1n
    \sin\qty(\frac{  2\pi n t}{T})
\end{equation}

## From Trig to Exponentials

It would be nice if we could convert this trigonometric series to a geometric series, which would make it easier for us to manipulate. Can we do that?

From Euler's formula, $$e^{i \phi} = \cos\phi + i \sin\phi$$, we could rewrite this series as
\begin{equation}\label{eq:sw2}
  f(t) = \frac{4}{\pi} \Im \sum_{n\text{ odd}} \frac{1}{n} e^{i n \omega t}
\end{equation}
where I have let $$\omega = 2 \pi / T$$ for notational convenience.

## Getting Rid of $$1/n$$

If we could get rid of the $$1/n$$ term inside the sum, we would have a geometric series. Suppose we take a time derivative of $$f(t)$$. Just to be sure we don't run into any issues as the upper limit of the sum tends to infinity, let us use an explicit upper limit. That is, let
\begin{equation}\label{eq:g}
  g_N(t) = \frac{4}{\pi} \Im \sum_{m = 0}^N \frac{1}{1 + 2m} e^{i(1+2m)\omega t}
\end{equation}
so that $$f(t) = \lim_{N \to \infty} g_N(t)$$. There is no problem differentiating the finite series $$g_N(t)$$:
\begin{equation}\label{eq:gprime}
  g'\_N(t) = \frac{4}{\pi} \Im \sum_{m = 0}^N i \omega e^{i(1+2m)\omega t}
  = \frac{4\omega}{\pi} \Im \left( ie^{i\omega t} \sum\_{m=0}^N e^{i 2 m \omega t} \right)
\end{equation}
The series is geometric, with ratio $$r = e^{2i\omega t}$$; we know how to sum such series!
\begin{equation}\label{eq:gprimesum}
  g'\_N(t) = \frac{4 \omega}{\pi} \Im \left( ie^{i\omega t} \frac{1 - e^{i 2(N+1) \omega t}}{1 - e^{2i\omega t}} \right)
\end{equation}