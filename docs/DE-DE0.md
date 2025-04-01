{:menu DE}

# First-Order Ordinary Differential Equations

* toc
{:toc}

A linear first-order differential equation has the form
\begin{equation}\label{eq:DE1}
  \dv{y}{t} + p(t) y(t) = q(t)
\end{equation}
where $$t$$ is the independent variable, $$y(t)$$ is the dependent variable, and $$q(t)$$ is a forcing function. If $$q(t) = 0$$, the equation is **homogeneous**; if not, it is **nonhomogeneous**. For given functions $$p(t)$$ and $$q(t)$$, a solution requires the additional input of the value of $$y(t)$$ at some chosen initial time (typically $$t = 0$$). Under general conditions we will outline below, the solution $$y(t)$$ exists and is unique. In the following, I will typically use a prime to indicate differentiation with respect to the independent variable.

## The Method of Integrating Factors

One strategy for finding $$y(t)$$ is to seek to express the left-hand side of the equation as the total derivative of some function of $$t$$.

- To that end, let us suppose that $$P(t) = \int p(t)\dd{t}$$, where we may pick any constant of integration.
- Multiply the differential equation by $$\exp[P(t)]$$ to get $$ [e^{P(t)} y]' = e^{P(t)} q(t) $$.
- Integrate both sides with respect to time to get
\\[
    e^{P(t)} y(t) = Q(t) + c \equiv \int e^{P(t)} q(t) \dd{t}
\\]
- Multiply by $$e^{-P(t)}$$ to solve for $$y(t)$$:
\begin{equation}\label{eq:integrating-factor}
  y(t) = e^{-P(t)} (Q(t) + c)
\end{equation}
for arbitrary constant $$c$$.

## Existence and Uniqueness

We would like to know under what conditions a solution to the equation $$y' = f(t, y)$$, with $$y(t_0) = y_0$$ has a solution. If the $$f(t,y)$$ and $$\pdv{f}{y}$$ are continuous on a closed rectangle $$R$$ on the $$ty$$ plane and the point $$(t_0, y_0)$$ is inside $$R$$, then a solution $$y(t)$$ exists on some $$t$$ interval containing $$t_0$$ in its interior, and no more than one solution in $$R$$ on any $$t$$ interval that contains $$t_0$$.