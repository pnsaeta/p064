{:menu DE}


# Sturm-Liouville Theory

* toc
{:toc}

## Flashback

In discussing [Fourier Series](FO-FourierSeries.md), we ran into the **bilinear concomitant**, which arose when considering solutions to the differential equation
\begin{equation}\label{eq:old}
  \dv[2]{y}{x} = -\lambda y(x)
\end{equation}

Recall that we started with two solutions, $$y_1(x)$$ and $$y_2(x)$$, and then integrated the combination $$y_1 ^{*\prime\prime} y_2 - y_1^* y_2 ^{\prime\prime}$$ from $$a$$ to $$b$$, getting
\begin{equation} \label{eq:BC}
\left[ y\_1^{\prime\*} y\_2 - y_1^\* y_2^\prime \right]_a^b  =
  (\lambda_1^\* - \lambda_2) \int_a^b y\_1^\* y_2 \, dx
\end{equation}
from which we showed that the eigenvalues $$\lambda$$ were real and that when the bilinear concomitant (the left-hand side) vanished, the functions $$y_1(x)$$ and $$y_2(x)$$ were orthogonal in the sense defined by the integral of Eq.&nbsp;(\ref{eq:BC}).

## Generalization

Sturm-Liouville theory is the generalization of this approach to second-order differential equations of the form
\begin{equation}\label{eq:Sturm-Liouville}
  P(x) y ^{\prime\prime} + Q(x) y' + R(x) y = 0
\end{equation}
These equations may be put into **self-adjoint form**
\begin{equation}\label{eq:self-adjoint}
  \boxed{  \dv{}{x}\qty[ p(x) \dv{y}{x}] + r(x) y = -\lambda w(x) y }
\end{equation}
where $$w(x)$$ is a **weighting factor** that will end up being used in the definition of the inner product of two solutions. That is, we define the inner product as
\begin{equation}\label{eq:inner}
  \ev{f,g} = \int_a^b [f(x)]^* g(x) \, w(x) \, dx
\end{equation}
Letting the linear operator $$L$$ be defined by
\begin{equation}\label{eq:linop}
  L \, y = - \frac{1}{w(x)} \left(\dv{}{x}\qty[ p(x) \dv{y}{x}] + r(x) y \right)
\end{equation}
the original differential equation is cast in the form
\begin{equation}\label{eq:linop2}
  L\,y = \lambda y
\end{equation}
which looks a lot like Eq.&nbsp;(\ref{eq:old}). To show that $$L$$ is a **self-adjoint** operator, meaning that
\begin{equation}\label{eq:selfadjoint}
  \ev{Lf, g} = \ev{f, Lg}
\end{equation}
it suffices to integrate twice by parts:
\begin{align}
 \ev{Lf,g} &= \int_{a}^{b} - \frac{1}{w(x)} 
   \left(\dv{}{x} \qty[p(x) f'] + r(x) f \right)^{\star}
    w(x) g(x) \dd{x}  \\\ 
   &= -\int_{a}^{b}  \left(\dv{}{x} \qty[p(x) f'] + r(x) f\right)^{\star} g(x) \dd{x} \\\ 
   &= \left.-p(x) f^{\star\prime}g\right|\_{a}^{b} + \int_{a}^{b} f^{\star\prime} p(x) g(x) \dd{x} -
    \int_{a}^{b} r(x) f^{\star} g \dd{x} \\\ 
    &= \left.-p(x) f^{\star\prime}g\right|\_{a}^{b} +
       \left. f^{\star} p(x) g' \right|\_{a}^{b} -
       \int_{a}^{b} f^{\star} \dv{}{x}\qty[ p(x) g'] \dd{x} -
       \int_{a}^{b} q(x) f^{\star} g \dd{x} \\\ 
       &=  \textcolor{DarkRed}{ 
        \underbrace{\left.p(x) \left( f^{\star}g' - f^{\star\prime}g \right) \right|\_{a}^{b} }\_{\text{bilinear concomitant}}} + \ev{f,Lg}
\end{align}
Provided that the boundary conditions at $$a$$ and $$b$$ cause the terms in red to vanish, then $$\ev{Lf,g} = \ev{f,Lg}$$.

Once we have shown that $$L$$ is self-adjoint, it follows easily (again) that the eigenvalues $$\lambda$$ must be real and that the eigenfunctions corresponding to different eigenvalues must be orthogonal:
\begin{align}
  \ev{Lu_1, u_2} - \ev{u_1, L u_2}  &= 0 \notag \\\ 
  \lambda_1^{\star} \ev{u_1, u_2} - \lambda_2 \ev{u_1, u_2} &= 0 \notag \\\ 
  (\lambda_1^{\star} - \lambda_2) \ev{u_1, u_2} &= 0
\end{align}
If $$u_1 = u_2$$, then $$(\lambda_1^{\star} - \lambda_1) \ev{u_1, u_1} = 0$$, which shows that $$\lambda_1$$ must be real. If $$\lambda_1 \ne \lambda_2$$, then $$\ev{u_1, u_2} = 0$$.

## Getting to Self-Adjoint Form

If $$P'(x) = Q(x)$$ in Eq.&nbsp;(\ref{eq:Sturm-Liouville}), we're effectively done: $$r(x) = R(x) + \lambda$$ and $$w(x) = 1$$.

However, there are plenty of common second-order linear differential equations where $$P'(x) \ne Q$$. For example, Bessel's equation is
\begin{equation}\label{eq:Bessel}
  x^2 y^{\prime\prime} + x y' + (x^2 - \nu^2) y = 0
\end{equation}
so that $$P' = 2x \ne x = Q$$. Intuitively, we could solve this little problem by dividing the whole equation by $$x$$ to get
\\[
    x y^{\prime\prime} + y' + \qty(x - \frac{\nu^2}{x}) y = 0
\\]
which we can put in the form
\\[
    \dv{}{x} \qty[ x y' ] + x y = \frac{\nu^2}{x} y \, w(x)
\\]
where $$w(x) = x$$.

### General Case

When $$P' \ne Q$$, we are looking for a function $$w(x)$$ so that the Sturm-Liouville eigenvalue problem becomes
\begin{equation}\label{eq:mSL}
  w(x) L \, y(x) = w(x) \lambda y(x)
\end{equation}
Let
\begin{equation}\label{eq:w}
  w(x) = \frac{1}{P(x)} \exp \qty(\int^x \frac{Q(x')}{P(x')}\dd{x'} )
\end{equation}
then direct substitution shows that
\begin{equation}\label{eq:direct}
  w(x) L = p(x) \dv[2]{}{x} + q(x) \dv{}{x} + w(x) R(x)
\end{equation}
where
\begin{align}
  p(x) &= \exp \qty(\int^x \frac{Q(x')}{P(x')}\dd{x'}) \notag \\\ 
  q(x) &= \frac{Q(x)}{P(x)} \exp \qty(\int^x \frac{Q(x')}{P(x')}\dd{x'})
\end{align}