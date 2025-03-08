{:menu FO}


# An Application of Fourier Transforms

* toc
{:toc}

The differential equation describing the motion of a damped driven simple harmonic oscillator is
\begin{equation}\label{eq:DDSHO}
  m\ddot{x} + b\dot{x} + m\omega_0^2 x = F_0(t)
\end{equation}
where $$b$$ is the linear damping constant and $$m\omega_0^2 = k$$ is the spring constant. Dividing through by the mass and letting $$\beta \equiv b/2m$$, we get
\begin{equation}\label{eq:DDSHO2}
  \ddot{x} + 2\beta \dot{x} + \omega_0^2 x = \frac{F_0(t)}{m}
\end{equation}

In Engineering 79, you may have solved this equation using Laplace transforms. Here, we will use the Fourier transform. To take the Fourier transform, let us first take the transform of $$\dot{x}$$:
\\[
    \int_{-\infty}^{\infty} \dot{x} e^{i\omega t} \dd{t} =
    x e^{i\omega t} \bigg|\_{-\infty}^{\infty} - \int_{-\infty}^{\infty} x (i\omega) e^{i\omega t}\dd{t}
\\]
Assuming that $$x(t)$$ goes to zero as $$t \to \pm \infty$$, the integrated term vanishes and we get
\\[
    \text{FT} (\dot{x}) = -i\omega \tilde{x}(\omega)
\\]
You can readily verify that each time derivative brings down another factor of $$(-i\omega)$$, so that the Fourier transform of Eq.&nbsp;(\ref{eq:DDSHO2}) is
\begin{equation}\label{eq:FTDDSHO}
  [(-i\omega)^2 - 2 \beta i \omega + \omega_0^2] \tilde{x}(\omega) = \frac1m \tilde{F}_0(\omega)
\end{equation}
Solving for $$\tilde{x}$$, we have
\begin{equation}\label{eq:xtilde}
  \tilde{x}(\omega) = \frac{\tilde{F_0}/m}{\omega_0^2 - \omega^2 - 2 \beta i \omega}
  = \tilde{F}_0(\omega) \tilde{G}(\omega)
\end{equation}
where
\\[
    \tilde{F}_0(\omega) = \int\_{-\infty}^{\infty} F\_0(t) e^{i\omega t}\dd{t}
    \qquad\text{and}\qquad
    \tilde{G}(\omega) = \frac{1/m}{\omega_0^2 - \omega^2 - 2 \beta i \omega}
\\]

## Returning to the time domain

Equation (\ref{eq:xtilde}) gives the Fourier transform of the oscillator's position in terms of the Fourier transform of the forcing function $$F_0(t)$$. To see the behavior of the oscillator in the time domain, we now need to take the inverse Fourier transform:
\begin{align}
  x(t) &= \frac{1}{2\pi} \int_{-\infty}^\infty e^{-i\omega t} \int_{-\infty}^{\infty} \frac{F_0(t')/m}{\omega_0^2 - \omega^2 - 2 \beta i \omega} e^{i\omega t'} \dd{t'} \dd{\omega}
  \\\ 
  &= \int_{-\infty}^{\infty}\dd{t'} F_0(t') \; 
  \underbrace{ \frac{1}{2\pi m} \int_{-\infty}^{\infty} \dd{\omega} \frac{e^{-i\omega(t-t')}}{\omega_0^2 - \omega^2 - 2 \beta i \omega}}_{G(t-t')}
\end{align}
where I have interchanged the order of integration. To perform the integration over $$\omega$$, we can use a contour that closes on a semicircle at $$R \to \infty$$, either in the upper half-plane (if $$t' > t$$) or the lower half-plane (if $$t' < t$$). 

Where are the poles? At the zeros of $$\omega^2 + 2 \beta i \omega - \omega_0^2$$, which are
\\[
    \omega_{\pm} = -i\beta \pm \sqrt{-\beta^2 + \omega_0^2}
\\]
Let $$\omega_1 \equiv \sqrt{\omega_0^2 - \beta^2}$$. For an under-damped system, the radical is real, so the poles lie in the LHP at $$-i\beta \pm \omega_1$$. 

Hence, if $$t' > t$$, we can close in the UHP and get $$G(t'-t) = 0$$. On the other hand, if $$t > t'$$, we must close the contour in the LHP, which means that we traverse the contour in the negative direction and that we enclose the two poles. Hence, for $$t > t'$$ we get
\begin{equation}\label{eq:G}
  G(t-t') = \frac{-2 \pi i}{2\pi m} \times \sum \text{residues}
\end{equation}
We may write the integrand as
\\[
    -\frac{e^{-i\omega(t-t')}}{(\omega - \omega_+)(\omega - \omega_-)}
\\]
from which we infer that the residues are
\\[
    -\frac{e^{-i\omega_+(t-t')}}{(\omega_+ -\omega_-)} = -\frac{e^{-\beta(t-t')} e^{-i\omega_1(t-t') }}{2\omega_1} \qquad\text{and}\qquad
    -\frac{e^{i\omega_-(t-t')}}{\omega_- - \omega_+} = \frac{e^{-\beta(t-t')} e^{i\omega_1(t-t')}}{2\omega_1}
\\]
with sum
\\[
    \frac{e^{-\beta(t-t')}}{\omega_1} \frac{e^{i\omega_1(t-t')} - e^{-i\omega_1(t-t')}}{2}
    = i \frac{e^{-\beta(t-t')}}{\omega_1} \sin\big[\omega_1(t-t')\big]
\\]
so that
\begin{equation}
    G(t-t') = \begin{cases}
      \displaystyle\frac{e^{-\beta(t-t')}}{m\omega_1} \sin\big[\omega_1(t-t')\big] & t > t' \\\ 
      0 & t < t'
    \end{cases}
\end{equation}
and
\begin{equation}\label{eq:convo}
  x(t) = \int_{-\infty}^{t} F_0(t') G(t-t') \dd{t'}
\end{equation}

In other words, the actual response of the oscillator, $$x(t)$$, is the convolution of $$F_0$$ and $$G$$. The Green's function, $$G(t-t')$$ describes the contribution to the motion of the oscillator at time $$t$$ after it has been given a unit impulse at (the earlier) time $$t'$$.

## Example

Let's say that at $$t = 0$$ an oscillatory forcing function begins and operates for $$N$$ cycles:
\\[
    F(t) = \begin{cases}
      F_0 \sin(\Omega t) & 0 < t < \frac{2 \pi N}{\Omega} \\\ 
      0 & \text{otherwise}
    \end{cases}
\\]
Its Fourier transform is
\begin{align}
    \tilde{F}(\omega) &= \int_{0}^{2 \pi N/\Omega} F_0 \frac{e^{i\Omega t} - e^{-i\Omega t}}{2i} e^{i\omega t}\dd{t}
    \\\ 
    &= \frac{F_0}{2i} \bigg[ \frac{e^{i(\omega+\Omega)t}}{i(\omega+\Omega)} - \frac{e^{i(\omega-\Omega)t}}{i(\omega-\Omega)} \bigg]_0^{2\pi N/\Omega}
    \\\ 
    &= \frac{F_0}{2} \bigg[ \frac{e^{i 2\pi N \omega/\Omega}-1}{\omega-\Omega} - 
    \frac{e^{i 2\pi N \omega/\Omega}-1}{\omega + \Omega}\bigg]
    \\\ 
    &= F_0 \Omega \frac{e^{i 2 \pi N \omega/\Omega}-1}{\omega^2 - \Omega^2}
\end{align}

By the convolution theorem, 