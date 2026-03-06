{:menu FO}

# An Application of Fourier Transforms

* toc
{:toc}

## The Damped Driven SHO

The differential equation describing the motion of a damped, driven simple-harmonic oscillator is
\begin{equation}\label{eq:DDSHO}
  m\ddot{x} + b\dot{x} + m\omega_0^2 x = F_0(t)
\end{equation}
where $$b$$ is the linear damping constant and $$m\omega_0^2 = k$$ is the spring constant. Dividing through by the mass and letting $$\beta \equiv b/2m$$, we get
\begin{equation}\label{eq:DDSHO2}
  \ddot{x} + 2\beta \dot{x} + \omega_0^2 x = \frac{F_0(t)}{m}
\end{equation}

In Engineering 79, you may have solved this equation using Laplace transforms. Here, we will use the Fourier transform.

To take the Fourier transform, let us first take the transform of $$\dot{x}$$:
\\[
    \int_{-\infty}^{\infty} \dot{x} e^{i\omega t} \dd{t} =
    x e^{i\omega t} \bigg|\_{-\infty}^{\infty} - \int_{-\infty}^{\infty} (i\omega) x e^{i\omega t}\dd{t}
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

## Returning to the Time Domain

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
    = \frac{F_0}{2i} \int_0^{2\pi N/\Omega} \left(e^{i(\omega+\Omega)t} - e^{i(\omega-\Omega)t} \right)\dd{t}
    \\\
    &= \frac{F_0}{2i} \bigg[ \frac{e^{i(\omega+\Omega)t}}{i(\omega+\Omega)} - \frac{e^{i(\omega-\Omega)t}}{i(\omega-\Omega)} \bigg]_0^{2\pi N/\Omega}
    \\\
    &= -\frac{F_0}{2} \bigg[ \frac{e^{i 2\pi N \omega/\Omega}-1}{\omega-\Omega} -
    \frac{e^{i 2\pi N \omega/\Omega}-1}{\omega + \Omega}\bigg]
    \\\
    &= F_0 \Omega \frac{1-e^{i 2 \pi N \omega/\Omega}}{\omega^2 - \Omega^2}
\end{align}

Let's define
\begin{equation}\label{eq:cutoff}
  T = \frac{2\pi N}{\Omega}
\end{equation}
which is the time that the forcing function stops.

By the convolution theorem, then,
\begin{align}
  x(t) &= \frac{1}{2\pi} \int_{-\infty}^{\infty} \frac{F_0 \Omega}{m}
  \frac{e^{-i\omega t}}{\omega_0^2-\omega^2-2\beta i \omega} \frac{1-e^{i\omega T}}{\omega^2 - \Omega^2} \dd{\omega}  \notag
\end{align}

Evaluating this integral is somewhat tricky. Let's first clean up the integrand slightly:
\begin{equation}
  x(t) = -\frac{F_0 \Omega}{2 \pi m} \int_{-\infty}^{\infty}
    \frac{e^{-i\omega t} - e^{-i\omega(t-T)}}
    {(\omega-\omega_{+})(\omega-\omega_{-})(\omega-\Omega)(\omega+\Omega)} \dd{\omega}
\end{equation}
where $$\omega_{\pm} = \pm\omega_1 - i\beta$$. Writing the integrand this way shows that it has four first-order poles, two on the real axis on the path of integration, and two in the lower half-plane.

### Case 1: $$ t < 0$$

We can close the contour without adding anything to the integral with a giant semicircle in the upper half-plane. The poles at $$\omega=\omega_\pm$$ are in the LHP, so they contribute nothing. At $$\omega = \pm \Omega$$, the numerator vanishes because $$e^{\pm i\Omega T} = e^{\pm i \, 2\pi N} = 1$$. Hence, $$x(t) = 0$$ for $$t < 0$$. That's reassuring: we haven't started forcing the oscillator yet!

### Case 2: $$0 < t < T$$

In this case we must separate the terms in the numerator, since for the first one we must close in the LHP while for the second we must close in the UHP. For the first, we go around in the clockwise (negative) direction; for the second, we go around counterclockwise.

### Case 3: $$ t > T$$

Now we must close the contour in the lower half-plane. By the same argument as for case 1, the numerator vanishes and we get no contribution from the poles that lie on the real axis. However, our contour now encloses the two poles in the LHP, so we will need to evaluate them.

### Poles at $$\omega = \omega_\pm$$

When $$\omega \to \omega_+$$, the denominator becomes $$(\omega-\omega_+)\Delta_+$$, where $$\Delta_+$$ is
\\[
    \Delta_+ = (\omega_+ - \omega_-)(\omega_+^2-\Omega^2)
    = 2\omega_1 (\omega_1^2 - \Omega^2 - \beta^2 -2 \beta \omega_1 i) = 2 \omega_1 (\Gamma - 2 \beta \omega_1 i)
\\]
where I have defined
\\[
  \Gamma \equiv \omega_1^2 - \Omega^2 - \beta^2
\\]

When $$\omega \to \omega_-$$, it becomes $$(\omega-\omega_-)\Delta_-$$ where
\\[
    \Delta_- = -(\omega_+ - \omega_-)(\omega_-^2 - \Omega^2) = -2\omega_1 (\omega_1^2 - \Omega^2 - \beta^2 + 2 \beta \omega_1 i) = - 2 \omega_1(\Gamma + 2 \beta \omega_1 i)
\\]

Let us define
\begin{align}
  \Delta &= \sqrt{\Gamma^{2} + 4 \beta^{2}\omega_{1}^{2}} \label{eq:Delta} \\\
  \tan \varphi &= \frac{2\beta\omega_{1}}{\Gamma}
\end{align}
in terms of which we can express the denominators in polar form as
\begin{align*}
  \Delta_{+}
  &=
    2 \omega_{1}\Delta e^{-i\varphi}
  \\\
  \Delta_{-}
  &= -2\omega_{1}\Delta e^{i\varphi}
\end{align*}
The two exponentials have the same form, so I will work out the contribution to
$$x(t)$$ for $$e^{-i\omega t}$$ and get the second one by taking $$t \to t-T$$. Setting aside
the prefactor for the moment, the sum of the residues at $$\omega \to \omega_{\pm}$$ is
\begin{align*}
  S(t)
  &=
    \frac{e^{-i\omega_{+}t}}{(\omega_{+}-\omega_{-})\Delta e^{-i\varphi}} +
    \frac{e^{-i\omega_{-}t}}{(\omega_{-}-\omega_{+}) \Delta e^{i\varphi}}
  \\\
  &= \frac{e^{-\beta t}}{2\omega_{1} \Delta} \left( e^{-i(\omega_{1}t - \varphi)} -
    e^{i(\omega_{1}t-\varphi)}\right)
  \\\
  &= \frac{e^{-\beta t}}{2\omega_{1}\Delta} (-2i) \sin(\omega_{1}t-\varphi)
  \\\
  &= \frac{-i e^{-\beta t} \sin(\omega_{1}t - \varphi)}{\omega_{1}\Delta}
\end{align*}

Combining now with the prefactor and the factor of $$2\pi i$$ for the poles, we get
\begin{align*}
  x(t)
  &=
    - \frac{F_{0}\Omega}{2\pi m} (-2 \pi i) \frac{-i}{\omega_{1}\Delta}
    \left( e^{-\beta t} \sin(\omega_{1}t-\varphi) - e^{-\beta(t-T)}\sin(\omega_{1}(t-T) - \varphi) \right)
  \\\
  &= \frac{F_{0}\Omega}{m \omega_{1}\Delta}
    \left( e^{-\beta t} \sin(\omega_{1}t-\varphi) - e^{-\beta(t-T)}\sin(\omega_{1}(t-T) - \varphi) \right)
\end{align*}


Since case 3 is simpler (we get nothing from the poles on the real axis), we'll start there.
\begin{align}
  x(t) &= -\frac{F_0 \Omega}{2\pi m} (-2\pi i)\left(
    \frac{e^{-i\omega_+ t} - e^{-i\omega_+(t-T)}}{2 \omega_1 (\Gamma - 2\beta\omega_1 i)}
    - \frac{e^{-i\omega_- t} - e^{-i\omega_-(t-T)}}{2\omega_1(\Gamma+2\beta\omega_1 i)} \right)  \notag \\\
    &= \frac{i F_0 \Omega}{2\omega_1 m}
      \frac{1}{\Gamma^2 + 4 \beta^2 \omega_1^2}
     \left(
      (\Gamma + 2 \beta \omega_1 i)(e^{-i\omega_+t} - e^{-i\omega_+(t-T)})
      - (\Gamma - 2\beta\omega_1 i)(e^{-i\omega_-t} - e^{-i\omega_-(t-T)})
      \right) \notag
      \\\
    &= \frac{i F_0 \Omega}{2\omega_1 m}
      \frac{1}{\Gamma^2 + 4 \beta^2 \omega_1^2}
     \bigg(
      e^{-\beta t} \bigg[ (\Gamma + 2 \beta \omega_1 i)e^{-i\omega_1 t} -
      (\Gamma - 2 \beta \omega_1 i)e^{i\omega_1 t} \bigg]
      \notag \\\
    &\qquad\qquad
      - e^{-\beta(t-T)} \bigg[ (\Gamma + 2 \beta \omega_1 i) e^{-i\omega_1(t-T)}
      - (\Gamma - 2 \beta \omega_1 i) e^{i\omega_1(t-T)}
      \bigg]
      \bigg)\notag \\\
    &= \frac{i F_0 \Omega}{2\omega_1 m}
      \frac{1}{\Gamma^2 + 4 \beta^2 \omega_1^2}
     \bigg( e^{-\beta t} \bigg[\Gamma(-2i)\sin \omega_1 t +2\beta\omega_1 (2i)\cos\omega_1 t \bigg] \notag
    \\\
    &\qquad\qquad
    - e^{-\beta(t-T)} \bigg[\Gamma (-2i)\sin\omega_1(t-T) + 2\beta\omega_1 i (2) \cos \omega_1(t-T)
      \bigg] \bigg) \notag
\end{align}
Both terms in square brackets can be simplified if we define a phase factor
\begin{equation}\label{eq:phase}
  \tan\varphi = \frac{2\beta\omega_1}{\Gamma}
\end{equation}
and using $$\sin(a+b) = \sin a\cos b + \cos a\sin b$$:
\begin{equation}\label{eq:case3}
  x(t) = \frac{F_0 \Omega}{m\omega_1}
   \frac{1}{\sqrt{\Gamma^2 + 4 \beta^2 \omega_1^2}}
   \bigg(
    e^{-\beta t}\sin(\omega_1 t - \varphi) -
    e^{-\beta(t-T)}\sin(\omega_1(t-T) - \varphi)
   \bigg)
\end{equation}

Hence, we are left with worrying about the poles at $$\omega_\pm$$. For $$t < 0$$, we may close the contour along a semicircular path at $$R\to\infty$$ in the UHP. Since that path contains no poles, we get zero, as we must expect: the oscillator is quiet before we start the forcing function at $$t = 0$$.

For $$t > T$$, we must close in the LHP for the exponentials in the numerators to go to zero. But if $$0 < t < T$$, we have to separate numerator into two distinct integrals, because we have to close in opposite half planes for the two terms. In either case, the denominator goes to the same expression (apart from the term going to zero), so we can evaluate it first. When $$\omega \to \omega_+$$, the denominator becomes
\\[
    \Delta_+ = (\omega_+ - \omega_-)(\omega_+^2-\Omega^2)
    = 2\omega_1 (\omega_1^2 - \Omega^2 - \beta^2 -2 \beta \omega_1 i) = 2 \omega_1 (\Gamma^2 - 2 \beta \omega_1 i)
\\]
where I have defined $$\Gamma^2 \equiv \omega_1^2 - \Omega^2 - \beta^2$$, and when $$\omega \to \omega_-$$, it becomes
\\[
    \Delta_- = -(\omega_+ - \omega_-)(\omega_-^2 - \Omega^2) = -2\omega_1 (\omega_1^2 - \Omega^2 - \beta^2 + 2 \beta \omega_1 i) = - 2 \omega_1(\Gamma^2 + 2 \beta \omega_1 i)
\\]

When $$0 < t < 2 \pi / N$$, we get a contribution from the two poles in the LHP from the term proportional to $$e^{-i\omega t}$$ and nothing from the other exponential, whose contour we close in the UHP. Hence, the residue theorem yields
\begin{align}
  x(t) &= \frac{F_0 \Omega}{2\pi m} (-2 \pi i) \bigg( \frac{e^{-i\omega_+ t}}{2\omega_1 (\Gamma^2-2\beta\omega_1 i)}
   -  \frac{e^{-i\omega_- t}}{2 \omega_1 (\Gamma^2 + 2 \beta \omega_1 i)}
   \bigg)\notag
   \\\
   &= - \frac{F_0 \Omega i}{2 \omega_1 m} e^{-\beta t} \left( \frac{e^{-i\omega_1 t}}{\Gamma^2-2\beta\omega_1 i } - \frac{e^{i\omega_1 t}}{\Gamma^2+2\beta\omega_1 i} \right) \notag
   \\\
   &= - \frac{F_0 \Omega i}{2 \omega_1 m} \frac{ e^{-\beta t} }{\Gamma^4 + 4 \beta^2 \omega_1^2}
   \bigg( e^{-i \omega_1 t}(\Gamma^2 + 2 \beta \omega_1 i) - e^{i\omega_1 t}(\Gamma^2 - 2 \beta \omega_1 i) \bigg) \notag \\\
   &= - \frac{F_0 \Omega i}{2 \omega_1 m} \frac{ e^{-\beta t} }{\Gamma^4 + 4 \beta^2 \omega_1^2}
   \bigg( 4\beta\omega_1 i \cos(\omega_1 t) - 2 \Gamma^2 i \sin (\omega_1 t) \bigg) \notag \\\
   &= \frac{F_0 \Omega}{\omega_1 m} \frac{e^{-\beta t}}{\Gamma^4 + 4 \beta^2 \omega_1^2}
   \left[ \Gamma^2 \sin(\omega_1 t) - 2\beta\omega_1 \cos(\omega_1 t)\right]
\end{align}
