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

- we first compute the acceleration for the current (known) values ($$x, v$$)
- update the velocity by applying the acceleration for half the time step
- update the position for the full time step using the newly updated velocity value
- recompute the acceleration using the updated values ($$x,v$$) and use it to update $$v$$ for the remaining half time step.

**Symplectic integrators** use a different strategy to integrate
