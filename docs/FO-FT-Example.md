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