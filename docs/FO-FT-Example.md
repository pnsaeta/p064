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
\end{equation}
where
\\[
    \tilde{F}_0(\omega) = \int\_{-\infty}^{\infty} F\_0(t) e^{i\omega t}\dd{t}
\\]

## Returning to the time domain

Equation (\ref{eq:xtilde}) gives the Fourier transform of the oscillator's position in terms of the Fourier transform of the forcing function $$F_0(t)$$. To see the behavior of the oscillator in the time domain, we now need to take the inverse Fourier transform:
\begin{align}
  x(t) &= \frac{1}{2\pi} \int_{-\infty}^\infty e^{-i\omega t} \int_{-\infty}^{\infty} \frac{F_0(t')/m}{\omega_0^2 - \omega^2 - 2 \beta i \omega} e^{i\omega t'} \dd{t'} \dd{\omega}
  \\\ 
  &= \frac{1}{2\pi m} \int_{-\infty}^{\infty}\dd{t'} F_0(t') \; \int_{-\infty}^{\infty} \dd{\omega} \frac{e^{i\omega(t'-t)}}{\omega_0^2 - \omega^2 - 2 \beta i \omega}
\end{align}
where I have interchanged the order of integration. To perform the integration over $$\omega$$, we can use a contour that closes on a semicircle at $$R \to \infty$$, either in the upper half-plane (if $$t'-t > 0$$) or the lower half-plane (if $$t'-t < 0$$). 

Where are the poles? At the zeros of $$\omega^2 + 2 \beta i \omega - \omega_0^2$$, which are
\\[
    \omega_{\pm} = -i\beta \pm \sqrt{-\beta^2 + \omega_0^2}
\\]
Let $$\omega_1 \equiv \sqrt{\omega_0^2 - \beta^2}$$. For an under-damped system, the radical is real, so the poles lie in the LHP. 

