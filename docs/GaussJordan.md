{:menu LinAl}
{::comment}menu-start{:/comment}

<div class="dropdown">
<label id="hamburger-menu"><img id="hamburger" src="figs/hamburger.png"></label>
<div class="dropdown-content">
<ul>
<li><a href="SquareMatrices.html">Special square matrices</a></li>
<li><a href="GaussJordan.html">Gauss-Jordan elimination</a></li>
<li><a href="HilbertSpace.html">Hilbert spaces</a></li>
<li><a href="Diagonalization.html">Diagonalizing a matrix</a></li>
<li><a href="Eigenvectors.html">Eigenvalues, eigenvectors, and completeness</a></li>
<li><a href="NumericalLinearAlgebra.html">Numerical linear algebra in NumPy</a></li>
</ul>
</div>
</div>

{::comment}menu-end{:/comment}


# Gauss-Jordan Elimination

* toc
{:toc}

## Motivation
One can seek the inverse of a given square matrix $$\mat{A}$$ using
**Gauss-Jordan elimination**, which consists in writing $$\mat{A}$$
and $$\mat{I}$$ side-by-side and conducting identical row operations on both to
reduce $$\mat{A}$$ to $$\mat{I}$$. If this procedure can be completed
successfully, then the companion array that started out as $$\mat{I}$$ will have
been reduced to $$\mat{A}^{-1}$$. *Row operations* consist in multiplying a row
by a scalar value and adding it to another row. The procedure is easiest to
understand with an example.

Consider the matrix
\\[
  \mat{A} = \begin{pmatrix}
   1 & 2 & -3 \\\ 
   2 & -1 & 4 \\\ 
 -2 & 1 & 3 
 \end{pmatrix}
\\]
and suppose we seek to solve for the components of $$\vb{x}$$ such
that $$\mat{A}\vdot\vb{x} = \begin{pmatrix}1 & 0 & 0\end{pmatrix}^{\rm
  T}$$. That is, we want to solve
\\[
  \begin{pmatrix}
   1 & 2 & -3 \\\ 
   2 & -1 & 4 \\\ 
 -2 & 1 & 3 
 \end{pmatrix} \vdot \begin{pmatrix}
   x_1 \\\ x_2 \\\ x_3
   \end{pmatrix}
  = \begin{pmatrix} 1 \\\ 0 \\\ 0 \end{pmatrix}
\\]
for $$x_1, x_2, x_3$$. Written out longhand, this means solving the set of equations

\begin{align}
  x_1 + 2 x_2 - 3 x_3 &= 1 \\\ 
  2x_1 - x_2 + 4x_3 &= 0 \\\ 
  -2 x_1 + x_2 + 3x_3 &= 0
\end{align}
We can clearly multiply each of these equations by any nonzero constant without
affecting the solution. Similarly, we can also add multiples of one row to
another without affecting the solution. These two facts justify the procedure of
Gauss-Jordan elimination, in which we perform these row operations in a logical
order to transform $$\mat{A}$$ into $$\mat{I}$$ while simultaneously
transforming $$\mat{I}$$ into $$\mat{A}^{-1}$$.

## Procedure
To start, write $$\mat{A}$$ next to the $$3\times3$$ identity matrix:
\\[
\begin{pmatrix}
1 & 2 & -3 & | & 1 & 0 & 0 \\\ 
2 & -1 & 4 & | & 0 & 1 & 0 \\\ 
-2 & 1 & 3 & | & 0 & 0 & 1
\end{pmatrix}
\\]
In this case, $$a_{11}$$ is already the number 1, so we don't need to alter the first row; if it had a different value, we could start by dividing the first row by that value. Element $$a_{11}$$ is called the **pivot**.
To zero the first column of rows 2 and 3, we multiply the first row by $$-2$$ and 2, respectively, and add to get
\\[
\begin{pmatrix}1 & 2 & -3 &  | &  1 & 0 & 0 \\\ 
0 & -5 & 10 & | & -2 & 1 & 0 \\\ 
0 & 5 & -3  & | &  2 & 0 & 1\end{pmatrix}
\\]
Now divide the second row by $$-5$$ to get
\\[
\begin{pmatrix}
1 & 2 & -3 &  | &  1 & 0 & 0 \\\ 
0 & 1 & -2 & | & 2/5 & -1/5 & 0 \\\ 
0 & 5 & -3  & | &  2 & 0 & 1
\end{pmatrix}
\\]
To eliminate the 5 on the second column of the third row, multiply the second row by $$-5$$ and add, giving
\\[
\begin{pmatrix}1 & 2 & -3 & | &  1 & 0 & 0 \\\ 
0 & 1 & -2 & | & 2/5 & -1/5 & 0 \\\ 
0 & 0 &  7 & | & 0 & 1 & 1\end{pmatrix}
\\]
Dividing the last row by 7 reduces the original matrix to standard upper-triangular form (ones on the main diagonal and zeros below it):
\\[
\begin{pmatrix}
1 & 2 & -3 & | &  1 & 0 & 0 \\\ 
0 & 1 & -2 & | & 2/5 & -1/5 & 0 \\\ 
0 & 0 &  1 & | & 0 & 1/7 & 1/7
\end{pmatrix}
\\]
Now we proceed from bottom to top, eliminating with row operations the nonzero entries above the main diagonal. Multiplying the final row by 2 and adding to the middle row gives
\\[
\begin{pmatrix}
1 & 2 & -3 & | &  1 & 0 & 0 \\\ 
0 & 1 &  0 & | & 2/5 & 3/35 & 2/7 \\\ 
0 & 0 &  1 & | & 0 & 1/7 & 1/7
\end{pmatrix}
\\]
We now add to the first row the second row multiplied by $$-2$$ and the third row multiplied by 3, which gives
\\[
\begin{pmatrix}
1 & 0 & 0 & | &  1/5 & 9/35 & -1/7 \\\ 
0 & 1 & 0 & | & 2/5 & 3/35 & 2/7 \\\ 
0 & 0 & 1 & | & 0 & 1/7 & 1/7
\end{pmatrix}
\\]
Thus, we have determined that 
\\[
  \mat{A}^{-1} = \begin{pmatrix}
  \frac15 & \frac{9}{35} & -\frac17 \\\ 
  \frac25 & \frac{3}{35} & \frac27 \\\ 
  0       & \frac17      & \frac17
 \end{pmatrix}
\\]
You may confirm that multiplying $$\mat{A}$$ by $$\mat{A}^{-1}$$ does indeed produce the identity matrix.

## Numerical Approach

Gauss-Jordan elimination is straightforward to program. A naïve implementation would proceed just as I have in the example. However, especially as the **rank** of the matrix to invert gets large, the method is numerical unstable and prone to numerical round-off error. Fortunately, it isn't too hard to adjust the procedure to avoid this instability. The trick is called (partial) pivoting and involves exchanging rows to put the largest potential pivot in the pivot row. How does this work. Let's start back at the beginning and scan the first column to look for the row with whose first element has the greatest magnitude:
\\[
\begin{pmatrix}
1 & 2 & -3 & | & 1 & 0 & 0 \\\ 
2 & -1 & 4 & | & 0 & 1 & 0 \\\ 
-2 & 1 & 3 & | & 0 & 0 & 1
\end{pmatrix}
\\]
In this case, there is a tie between the second and third rows. I will pick row 2 and exchange rows 1 and 2, to get
\\[
\begin{pmatrix}
2 & -1 & 4 & | & 0 & 1 & 0 \\\ 
1 & 2 & -3 & | & 1 & 0 & 0 \\\ 
-2 & 1 & 3 & | & 0 & 0 & 1
\end{pmatrix}
\\]
Dividing the first row by 2 and then using it to zero the first column of rows 2 and 3 gives
\\[
\begin{pmatrix}
1 & -1/2 & 2 &  | & 0 & 1/2  & 0 \\\ 
0 & 5/2  & -5 & | & 1 & -1/2 & 0 \\\ 
0 & 0    & 7 &  | & 0 & 1    & 1
\end{pmatrix}
\\]
Now multiply the second row by $$2/5$$ (and the final row by $$1/7$$):
\\[
\begin{pmatrix}
1 & -1/2 & 2 &  | & 0 & 1/2  & 0 \\\ 
0 & 1  & -2 & | & 2/5 & -1/5 & 0 \\\ 
0 & 0    & 1 &  | & 0 & 1/7  & 1/7
\end{pmatrix}
\\]
Use the final row to zero the final column of rows 1 and 2:
\\[
\begin{pmatrix}
1 & -1/2 & 0 & | & 0 & 3/14  & -2/7 \\\ 
0 & 1    & 0 & | & 2/5 & 3/35 & 2/7 \\\ 
0 & 0    & 1 & | & 0 & 1/7  & 1/7
\end{pmatrix}
\\]
Finally, multiply row 2 by $$1/2$$ and add it to the first row
\\[
\begin{pmatrix}
1 & 0 & 0 & | & 1/5 & 9/35 & -1/7 \\\ 
0 & 1 & 0 & | & 2/5 & 3/35 & 2/7 \\\ 
0 & 0 & 1 & | & 0   & 1/7  & 1/7
\end{pmatrix}
\\]
which yields the same result for the inverse as before.
