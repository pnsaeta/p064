{:menu PR}

# Simulating Physical Systems

* toc
{:toc}

Almost every quantity we use to describe a physical system combines both a numerical value and a unit. Even angles sort of qualify: we could be using degrees instead of radians, for instance. (The exception is counting numbers, such as how many particles are in the system.)

In most cases, however, there are "natural scales" you can and should use to remove dimensions from your simulations and yield quantities that are neither extremely large nor extremely small compared to 1. I think the easiest way to see how to do this is to look at an example system.

Let's model a set of $$N$$ identical simple pendulums of length $$\ell$$ and mass $$m$$ mounted atop a plank of mass $$M$$. The pendulums oscillate in the $$xz$$ plane, each one described by an angle $$\theta_j$$ with respect to vertically down. The plank, in turn, is placed on rollers so that it can move freely in the $$x$$ direction. With a little work, you can show that the kinetic and potential energies are
\begin{align}
  T &= \frac12 \left(M + Nm \right) \dot{x}^2 +
  m\ell \dot{x} \sum_j \dot{\theta}_j \,\cos\theta_j +
  \frac12 m \ell^2 \sum_j \dot{\theta}_j^2 \\\
  U &= - m g \ell \sum_j \cos\theta_j
\end{align}
These expressions have two masses ($$m$$ and $$M$$), two lengths ($$x$$ and $$\ell$$), and a bunch of angles. How can we simplify?

Let's first express the mass of the plank in terms of the mass of a pendulum by defining
\begin{equation}
  M \equiv \mu m
\end{equation}
and divide both equations by $$m$$. Then we have
\begin{align}
  T/m &= \frac12 \left(\mu + N \right) \dot{x}^2 +
  \ell \dot{x} \sum\_j \dot{\theta}\_j \,\cos\theta\_j +
  \frac12  \ell^2 \sum\_j \dot{\theta}\_j^2 \\\
  U/m &= - g \ell \sum\_j \cos\theta\_j
\end{align}
Let's now use the pendulum length $$\ell$$ as the standard of distance by defining
\begin{equation}\label{eq:pr-def-y}
  x \equiv y \ell
\end{equation}
Making this substitution and dividing both sides by $$\ell^2$$ gives
\begin{align}
  T/m\ell^2 &= \frac12 \left(\mu + N \right) \dot{y}^2 +
    \dot{y} \sum\_j \dot{\theta}\_j \,\cos\theta\_j +
  \frac12  \sum\_j \dot{\theta}\_j^2 \\\
  U/m\ell^2 &= - \frac{g}{\ell} \sum\_j \cos\theta\_j
\end{align}
That's looking much better. But, we recognize $$g/\ell = \omega^2$$ as the angular frequency squared of the small-angle oscillations of one of the pendulums. That seems to be a sensible way to scale time. So, let's define
\begin{equation}
  \tau \equiv \omega t = \sqrt{g/\ell}\; t
\end{equation}
Then a derivative with respect to "real" time $$t$$ is
\begin{equation*}
    \dv{}{t} = \omega \dv{}{\tau}
\end{equation*}
I'll now use a prime to represent differentiation with respect to $$\tau$$, to get
\begin{align}
  T/m\ell^2 &= \frac12 \omega^2\left(\mu + N \right) {y'}^2 +
    \omega^2 y' \sum\_j \theta'\_j \,\cos\theta\_j +
  \frac12 \omega^2 \sum\_j (\theta'\_j)^2 \\\
  U/m\ell^2 &= - \omega^2 \sum\_j \cos\theta\_j
\end{align}
Putting things together to make the lagrangian, $$L = T-U$$, and noting that multiplying the lagrangian by a constant leaves the equations of motion unchanged (so can can drop $$m \ell^2 \omega^2$$ from each term), we have
\begin{equation}\label{eq:pr-lagrangian}
  \boxed{ L = \frac12(\mu+N) \dot{y}^2 + \sum_{j=1}^N \left[ (\dot{y}\dot{\theta}_j + 1)\cos\theta_j +
   \frac12 \dot{\theta}_j^2 \right] }
\end{equation}
where $$y = x/\ell$$, $$\mu = M/m$$, and $$\tau = \sqrt{g/\ell}\; t$$, and I have reverted to dot notation to indicate differentiation with respect to the time variable $$\tau$$.

To get the equations of motion, we use the usual Euler-Lagrange equations:
\begin{equation}\label{eq:pr-euler-lagrange}
  \dv{}{t} \left(\pdv{L}{\dot{q}_i} \right) = \pdv{L}{q_i}
\end{equation}
for each coordinate $$q_i$$.
