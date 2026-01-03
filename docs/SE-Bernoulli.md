{:menu SE}

# Bernoulli Numbers

* toc
{:toc}

Unless Vatche provides a reasonable justification, I suspect I'll omit this section!

The Bernoulli numbers $$B_n$$ arise in many computational physics problems; they may be defined by 
\\[
    \frac{t}{e^t-1} = \sum\_{n=0}^\infty \frac{B\_n t^n}{n!}
\\]
One way to work out the first few Bernoulli numbers is to multiply both sides by $$(e^t-1)/t$$ to get
\begin{align}
  1 &= t^{-1} \qty(e^t - 1) \qty(B\_0 + B\_1 t + \frac{B\_2 t^2}{2!} + \cdots) \notag \\\ 
  1 &= \qty(1 + \frac{t}{2!} + \frac{t^2}{3!} + \cdots)\qty(B\_0 + B\_1 t + \frac{B\_2 t^2}{2!} + \cdots) \notag
\end{align}
The only term on the right that has $$t^0$$ in it is $$B_0$$, so we deduce that $$B_0 = 1$$.
There are two terms that involve $$t^1$$, which gives
\\[
    0 = B_0 \frac{t}{2} + B_1 t = \qty(\frac{B_0}{2} + B_1)t 
    \longrightarrow B_1 = -\frac12
\\]
Gathering terms proportional to $$t^2$$ yields
\\[
    0 = \qty(\frac{B\_0 }{3!} + \frac{B\_1}{2!} + \frac{B\_2}{2!} )t^2
    = \qty( \frac16 - \frac14 + \frac{B\_2}{2})t^2 \longrightarrow B\_2 = \frac16
\\]

A routine to compute the first $$n$$ Bernoulli numbers is available in `scipy.special.bernoulli`:

~~~~ python
from scipy.special import bernoulli

bernoulli(6)
array([ 1.        , -0.5       ,  0.16666667,  0.        , -0.03333333,
        0.        ,  0.02380952])
~~~~

As you can probably guess from this output, the Bernoulli numbers for odd $$n \ge 3$$ all vanish.