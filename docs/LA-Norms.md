{:menu LA}

# The Norm of a Vector Space

* toc
{:toc}

I previously claimed that the **norm** of a vector in a space with a defined inner product is
\begin{equation}
  \Vert \vb{a} \Vert = \sqrt{\langle \vb{a}, \vb{a} \rangle}
\end{equation}
and this is indeed a satisfactory form. However, other definitions are possible, consistent with the following properties:

1. $$||\vb{v}|| \ge 0$$ ; $$||\vb{v}|| = 0$$
   if and only if $$\vb{v} = \vb{0}$$.

2. $$ \Vert\alpha \mathbf{v}\Vert = $$
   $$ |\alpha| \Vert\vb{v}\Vert $$.

3. $$ \Vert\vb{v}_1 + \vb{v}_2\Vert \le \Vert\vb{v}_1\Vert + \Vert\vb{v}_2\Vert $$ (the triangle inequality).

## Examples

1. $$\Vert (a_1, \ldots, a_n) \Vert = \sqrt{ \sum_{k=1}^n |a_k|^2}$$

2. $$\Vert (a_1, \ldots, a_n) \Vert = \sum_{k=1}^n |a_k| $$