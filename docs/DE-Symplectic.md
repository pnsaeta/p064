{:menu DE}

# Symplectic Integrators

* toc
{:toc}

We saw [on the page describing how to solve second-order ODEs numerically](DE-DE3) that the trick is to rewrite them as systems of coupled first-order ODEs and use a solver such as `scipy.integrate.solve_ivp` to perform the integration while simultaneously bounding the error. In practice, it may take some fiddling with the integration method and the error tolerances `rtol` and `atol` to obtain acceptable results.

As Prof. Tamayo can readily explain, however, the Runge-Kutta solvers available in `solve_ivp` have a property that makes them less than ideal for integrating equations of motion over very extended periods. To illustrate, let's repeat our simulation of the simple harmonic oscillator and focus not so much on $$x(t)$$ but on the sum of kinetic and potential energy in the computed solution. The system is clearly conservative, so we should expect the energy to remain constant. Let's see.

~~~~ python
def SHOderiv(t, Y, k, m):
    x, v = Y
    return (v, -k * x / m)

k, m = 1, 1
s = solve_ivp(SHOderiv, (0, 100), (np.sqrt(2),0), t_eval=np.arange(0, 100, 0.1),
              rtol=1e-6, atol=1e-6, method='RK45', args=(k, m))
# Compute the oscillator energy
x = s.y[0,:]
v = s.y[1,:]
E = 0.5 * (k * x**2 + m * v**2)
fig, ax = plt.subplots()
ax.plot(s.t, E);
~~~~

<p class="figure" markdown="0">
  <img src="figs/RK-energy.webp" style="width: 400px;" alt="Energy leakage using a Runge-Kutta solver">
</p>
<p class="icap" markdown="1"><a name="Fig1">Figure 1</a> — The sum of kinetic and potential energy in a numerical solution of the SHO equation of motion. Tightening the tolerances reduces the scale of the error but not the general downward trend.</p>

## Leapfrog

In Runge-Kutta integrators, all dependent variables are updated in parallel. That is, at each (sub) time step, all derivatives are computed and used to advance each dependent variable. By contrast, in the leapfrog approach,

- we first compute the acceleration using the current (known) values ($$x, v$$)
- update the velocity by applying the acceleration for half the time step: $$v \leftarrow v + \frac12 a \Delta t$$
- update the position for the full time step using the newly updated velocity value: $$x \leftarrow x + v \Delta t$$
- recompute the acceleration using the updated values ($$x,v$$) and use it to update $$v$$ for the remaining half time step: $$v \leftarrow v + \frac12 a \Delta t$$.

The method is called leapfrog, because we alternately update the position and the velocity, using always the most recent values of $$(x,v)$$ for the updates.

## Symplectic methods

More generally, a **symplectic integrator** subdivides a time step $$\Delta t$$ into $$k$$ parts, and for each part, updates first the velocity and then the position using the equations
\begin{align}
  v_i &= v_{i-1} + (\Delta t) c_i a(x_{i-1})  \label{eq:vupdate} \\\
  x_i &= x_{i-1} + (\Delta t) d_i v_i \label{eq:xupdate}
\end{align}
The leapfrog method uses $$c_i = (\frac12, \frac12)$$ and $$d_i = (1, 0)$$ and is second order ($$k=2$$). Higher-order methods are possible, too. A third-order integrator uses $$c_i = (\frac{7}{24}, \frac34, -\frac{1}{24})$$ and $$d_i = (\frac23, -\frac23, 1)$$, and a fourth-order one uses ($$q \equiv 2^{1/3}$$)
\begin{align}
  c_1 = c_4 &= \frac{1}{2(2-q)} \\\
  c_2 = c_3 &= \frac{1-q}{2(2-q)} \\\
  d_1 = d_3 &= \frac{1}{2-q} \\\
  d_2 &= - \frac{q}{2-q} \\\
  d_4 &= 0
\end{align}

<p class="figure" markdown="0">
  <img src="figs/Symplectic-energy.webp" style="width: 400px;" alt="Failure of energy conservation">
</p>
<p class="icap" markdown="1"><a name="Fig2">Figure 2</a> — The degree of energy nonconservation, $$|E - E_0|$$, as a function of time for the simple harmonic oscillator integrated with the RKF45 method by `solve_ivp` and by symplectic integrators of order $$k$$. The RKF45 routine uses an adaptive step size to bound the error, whereas the symplectic integrators all used a step size $$\Delta t = 0.05$$. Unlike the Runge-Kutta method, the energy errors of the symplectic integrators </p>

Next: [Quantum SHO](DE-SHO-analytic.md)
