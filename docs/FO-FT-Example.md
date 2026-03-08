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
      F_0 \sin(\Omega t) & 0 < t < \frac{2 \pi N}{\Omega} \equiv T \\\
      0 & \text{otherwise}
    \end{cases}
\\]
Note that $$T$$ is the time when the forcing function ceases.
The Fourier transform  of $$F(t)$$ is
\begin{align}
    \tilde{F}(\omega) &= \int_{0}^{T} F_0 \frac{e^{i\Omega t} - e^{-i\Omega t}}{2i} e^{i\omega t}\dd{t}
    = \frac{F_0}{2i} \int_0^{T} \left(e^{i(\omega+\Omega)t} - e^{i(\omega-\Omega)t} \right)\dd{t}
    \\\
    &= \frac{F_0}{2i} \bigg[ \frac{e^{i(\omega+\Omega)t}}{i(\omega+\Omega)} - \frac{e^{i(\omega-\Omega)t}}{i(\omega-\Omega)} \bigg]_0^{T}
    \\\
    &= -\frac{F_0}{2} \bigg[ \frac{e^{i\omega T}-1}{\omega+\Omega} -
      \frac{e^{i\omega T}-1}{\omega - \Omega}
      \bigg]
      \\\
    &= -\frac{F_0}{2} (e^{i\omega T}-1)\bigg[
      \frac{\omega-\Omega - \omega - \Omega}{\omega^2 - \Omega^2}
        \bigg]
        \\\
    &= F_0 \Omega \frac{e^{i \omega T}-1}{\omega^2 - \Omega^2}
\end{align}

By the convolution theorem, then,
\begin{align}
  x(t) &= \frac{1}{2\pi} \int_{-\infty}^{\infty} \frac{F_0 \Omega}{m}
  \frac{e^{-i\omega t}}{\omega_0^2-\omega^2-2\beta i \omega} \frac{e^{i\omega T} - 1}{\omega^2 - \Omega^2} \dd{\omega}  \notag
\end{align}

Evaluating this integral is somewhat tricky. Let's first clean up the integrand slightly by shifting the denominator to have positive $$\omega^2$$ in the first denominator and flipping the sign of the final numerator:
\begin{equation}
  x(t) = \frac{F_0 \Omega}{2 \pi m} \int_{-\infty}^{\infty}
    \frac{e^{-i\omega t} - e^{-i\omega(t-T)}}
    {(\omega-\omega_{+})(\omega-\omega_{-})(\omega-\Omega)(\omega+\Omega)} \dd{\omega}
\end{equation}
where $$\omega_{\pm} = \pm\omega_1 - i\beta$$. Writing the integrand this way shows that it has four first-order poles, two on the real axis on the path of integration, and two in the lower half-plane.

### Case 1: $$ t < 0$$

We can close the contour without adding anything to the integral with a giant semicircle in the upper half-plane. The poles at $$\omega=\omega_\pm$$ are in the LHP, so they contribute nothing. At $$\omega = \pm \Omega$$, the numerator vanishes because $$e^{\pm i\Omega T} = e^{\pm i \, 2\pi N} = 1$$. Hence, $$x(t) = 0$$ for $$t < 0$$. That's reassuring: we haven't started forcing the oscillator yet!

### Case 2: $$ t > T$$

Now we must close the contour in the lower half-plane. By the same argument as for case 1, we get no contribution from the poles that lie on the real axis because the numerator vanishes. However, our contour now encloses the two poles in the LHP, so we will need to evaluate them.

### Case 3: $$0 < t < T$$

In this case we must separate the terms in the numerator, since for the first one we must close in the LHP while for the second we must close in the UHP. For the first, we go around in the clockwise (negative) direction; for the second, we go around counterclockwise.

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
\begin{align}
  \Delta_{+}
  &=
    2 \omega_{1}\Delta e^{-i\varphi} \notag
  \\\
  \Delta_{-}
  &= -2\omega_{1}\Delta e^{i\varphi} \notag
\end{align}
The two exponentials have the same form, so I will work out the contribution to
$$x(t)$$ for $$e^{-i\omega t}$$ and get the second one by taking $$t \to t-T$$. Setting aside
the prefactor for the moment, the sum of the residues at $$\omega \to \omega_{\pm}$$ is
\begin{align}
  S(t)
  &=
    \frac{e^{-i\omega_{+}t}}{(\omega_{+}-\omega_{-})\Delta e^{-i\varphi}} +
    \frac{e^{-i\omega_{-}t}}{(\omega_{-}-\omega_{+}) \Delta e^{i\varphi}}
  \notag \\\
  &= \frac{e^{-\beta t}}{2\omega_{1} \Delta} \left( e^{-i(\omega_{1}t - \varphi)} -
    e^{i(\omega_{1}t-\varphi)}\right) \notag
  \\\
  &= \frac{e^{-\beta t}}{2\omega_{1}\Delta} (-2i) \sin(\omega_{1}t-\varphi)
  \notag \\\
  &= \frac{-i e^{-\beta t} \sin(\omega_{1}t - \varphi)}{\omega_{1}\Delta}
  \notag
\end{align}

Combining now with the prefactor and the factor of $$-2\pi i$$ for the poles, which we enclose while integrating in the negative sense, we get
\begin{align}
  x(t)
  &=
    - \frac{F_{0}\Omega}{2\pi m} (-2 \pi i) \frac{-i}{\omega_{1}\Delta}
    \left( e^{-\beta t} \sin(\omega_{1}t-\varphi) - e^{-\beta(t-T)}\sin(\omega_{1}(t-T) - \varphi) \right)
  \notag\\\
  &= \frac{F_{0}\Omega}{m \omega_{1}\Delta}
    \left( e^{-\beta t} \sin(\omega_{1}t-\varphi) - e^{-\beta(t-T)}\sin(\omega_{1}(t-T) - \varphi) \right) \label{eq:case3}
\end{align}
This is the entire solution for case 3, since we get nothing from the poles on the real axis.


When $$0 < t < T$$, we get a contribution from the two poles in the LHP from the term proportional to $$e^{-i\omega t}$$ and nothing from the other exponential, whose contour we close in the UHP. So, the poles in the LHP yield Eq.\eqref{eq:case3} without the term involving $$t-T$$, to which we must add the contributions from the poles on the real axis.

Again setting aside the prefactor for the moment, we need to evaluate
\begin{equation}
  I(t) = \int_{-\infty}^{\infty}
    \frac{e^{-i\omega t} }
    {(\omega-\omega_{+})(\omega-\omega_{-})(\omega-\Omega)(\omega+\Omega)} \dd{\omega}
\end{equation}
at $$\omega \to \pm \Omega$$.
The residue at $$\omega \to -\Omega$$ is
\begin{align}
    a_{-1}(-\Omega) &= \frac{e^{i\Omega t}}{(-\Omega-\omega_+)
    (-\Omega-\omega_-)(-2\Omega)}
    \notag \\\
    &= -\frac{e^{i\Omega t}}{(2\Omega)(\Omega^2 + \omega_+\omega_- + \Omega(\omega_+ + \omega_-))}
    \notag \\\
    &= - \frac{e^{i\Omega t}}{(2\Omega)( \Omega^2 -\omega_1^2 -\beta^2 - 2 \beta \Omega i)}
    \notag \\\
    &= - \frac{e^{i\Omega t}}{(2\Omega)\Delta e^{-i\varphi}}
    = -\frac{e^{i(\Omega t + \varphi)}}{2\Omega\Delta}
    \label{eq:resn}
\end{align}
and the residue at $$\omega \to \Omega$$ is
\begin{align}
    a_{-1}(\Omega) &= \frac{e^{-i\Omega t}}{(\Omega-\omega_+)
    (\Omega-\omega_-)(2\Omega)}
    \notag \\\
    &= \frac{e^{-i\Omega t}}{(2\Omega)(\Omega^2 + \omega_+\omega_-
    - \Omega(\omega_+ + \omega_-))}
    \notag \\\
    &= \frac{e^{-i\Omega t}}{(2\Omega)( \Omega^2 -\omega_1^2 -\beta^2
     + 2 \beta \Omega i)}
    \notag \\\
    &= \frac{e^{-i\Omega t}}{(2\Omega)\Delta e^{i\varphi}}
    = \frac{e^{-i(\Omega t + \varphi)}}{2\Omega\Delta}
    \label{eq:resp}
\end{align}

Since $$t > 0$$, we can close in the LHP and get $$-i\pi$$ times the sum of the residues. Hence, from the first exponential, we get a contribution to $$x(t)$$ of
\begin{align}
  x_1(t) &= -\frac{F_0\Omega}{2\pi m} (-\pi i) \frac{-e^{i(\Omega t+\varphi)}
  + e^{-i(\Omega t + \varphi)}}{2\Omega\Delta}
    \notag \\\
    &= \frac{F_0}{2 m \Delta} (i) (-i \sin(\Omega t + \varphi))
    = \frac{F_0 \sin(\Omega t + \varphi)}{m \Delta}
    \notag
\end{align}

For the term with $$e^{-i\omega(t-T)} = e^{i\omega(T-t)}$$ in the numerator, we close in the UHP and get $$\pi i$$ times the sum of the residues:
\\[
    x_2(t) = \frac{F_0 \sin(\Omega(t-T)+\varphi)}{m\Delta}
\\]

## Solution

Let's reprise the definitions we've made:
\begin{align}
  \beta &= \frac{b}{2m}  \notag \\\
  \omega_0 &= \sqrt{k/m} \notag \\\
  T &= \frac{2\pi N}{\Omega} \notag \\\
  \omega_1 &= \sqrt{\omega_0^2 - \beta^2} \notag \\\
  \omega_{\pm} &= -i\beta \pm \omega_1 \notag \\\
  \Gamma &= \omega_1^2 - \Omega^2 - \beta^2 \notag \\\
  \Delta &= \sqrt{\Gamma^2 + 4 \omega_1^2 + \beta^2} \notag \\\
  \tan \varphi &= \frac{2 \omega_1 \beta}{\Gamma} \notag \\\
  \gamma &= \Omega^2 - \omega_0^2 \notag \\\
  \delta &= \sqrt{\gamma^2 + 4 \beta^2 \Omega^2} \notag \\\
  \tan \psi &= \frac{2 \beta \Omega}{\gamma} \notag
\end{align}

In terms of these definitions, the solution for $$x(t)$$ is
\begin{equation}\label{eq:amazing}
  x(t) = \begin{cases}
  0 & t < 0 \\\
  -\frac{F_0}{m}\bigg[
    \frac{\Omega}{\Delta\omega_1} e^{-\beta t}\sin(\omega_1 t - \varphi)
    + \frac{\sin(\Omega t + \psi)}{\delta}
  \bigg] & 0 \le t \le T
  \\\
  \frac{F_0 \Omega}{m \omega_1 \Delta}\bigg[
    e^{-\beta(t-T)} \sin\big[\omega_1(t-T)-\varphi\big]
    - e^{-\beta t} \sin(\omega_1 t - \varphi)
  \bigg] & t > T
  \end{cases}
\end{equation}
