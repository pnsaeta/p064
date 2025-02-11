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

