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

One strategy for finding $$y(t)$$ is to seek to express the left-hand side of the equation as the total derivative of some function of $$t$$. To that end, let us suppose that $$P(t) = \int p(t)\dd{t}$$, where we may pick any constant of integration.