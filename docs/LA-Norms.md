{:menu LA}

# The Norm of a Vector Space

* toc
{:toc}

I previously claimed that the **norm** of a vector in a space with a defined inner product is
\begin{equation}
  \Vert \vb{a} \Vert = \sqrt{\ev{\vb{a},\vb{a}}}
  \label{eq:spnorm}
\end{equation}
and this is indeed a satisfactory form. However, other definitions are possible, consistent with the following properties:

1. $$||\vb{v}|| \ge 0$$ ; $$||\vb{v}|| = 0$$
   if and only if $$\vb{v} = \vb{0}$$.

2. $$ \Vert\alpha \mathbf{v}\Vert = $$
   $$ |\alpha| \Vert\vb{v}\Vert $$.

3. $$ \Vert\vb{v}_1 + \vb{v}_2\Vert \le \Vert\vb{v}_1\Vert + \Vert\vb{v}_2\Vert $$ (the triangle inequality).

## Examples

\begin{align}
    \Vert (a\_1, \ldots, a\_n) \Vert &= \sqrt{ \sum_{k=1}^n |a\_k|^2} \\\ 
    \Vert (a\_1, \ldots, a\_n) \Vert &= \sum\_{k=1}^n |a\_k| \label{eq:USPS} \\\ 
    \Vert (a\_1, \ldots, a\_n) \Vert &= \text{max}\_{k=1}^n |a\_k|  \\\ 
    \Vert (a\_1, \ldots, a\_n) \Vert &= \text{max}\_{k=1}^n k|a\_k|
\end{align}

You may confirm that each of these definitions satisfies all three required properties to be a norm.
As Nearing points out, "the United States Postal Service prefers a variation on Eq.&nbsp;(\ref{eq:USPS}), which makes good sense in a place like Manhattan, though not as much in Boston.

## Scalar Products

A scalar product is a scalar function of two vectors with the following properties:

1. $$\ev{\vb{w},(\vb{u} + \vb{v})} = \ev{\vb{w}, \vb{u}} + \ev{\vb{w}, \vb{v}}$$.

2. $$\ev{\vb{w}, \alpha\vb{v}} = \alpha \ev{\vb{w}, \vb{v}}$$.

3. $$\ev{\vb{u}, \vb{v}}^{*} = \ev{\vb{v}, \vb{u}}$$.

4. $$\ev{\vb{v}, \vb{v}} \ge 0;\quad\text{and}\quad \ev{\vb{v}, \vb{v}} = 0$$ if and only if
   $$\vb{v} = \vb{0}$$.

If a scalar product is defined on a particular vector space, then a natural definition for norm is the one we started with in Eq.&nbsp;(\ref{eq:spnorm}). However, consistency requires us to show that this norm satisfies the triangle inequality.

### Example Scalar Product

We argued that cubic polynomials on $$0 \le x \le 1$$ form a vector space, in which the basis vectors could be taken to be $$(1, x, x^2, x^3)$$, the addition of vectors and scalar multiplication are as expected:
\begin{align}
    (a_0 + a_1 x + a_2 x^2 + a_3 x^3) + (b_0 + b_1 x + b_2 x^2 + b_3 x^3) &=
    (a_0 + b_0) + (a_1 + b_1) x + (a_2 + b_2) x^2 + (a_3 + b_3) x^3
    \\\ 
    \alpha (a_0 + a_1 x + a_2 x^2 + a_3 x^3) &= (\alpha a_0) + (\alpha a_1) x + (\alpha a_2) x^2 + (\alpha a_3) x^3
\end{align}

What could be a scalar product for this vector space? Consider
\begin{equation}
    \ev{f, g} = \int_0^1 f(x) g(x) \dd{x}
\end{equation}

## Cauchy-Schwartz Inequality

The **Cauchy-Schwartz inequality** is
\begin{equation} \label{eq:cauchy-schwartz}
  |\ev{\vb{u}, \vb{v}}| \le \Vert\vb{u}\Vert  \Vert\vb{v}\Vert
\end{equation}
You can prove it by considering
$$ \ev{\vb{u} - \lambda \vb{v}, \vb{u} - \lambda \vb{v}} \ge 0 $$, where $$\lambda$$ is an arbitrary scalar.