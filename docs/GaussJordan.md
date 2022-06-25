# Gauss-Jordan Elimination

One can seek the inverse of a given square matrix $$\mat{A}$$ using **Gauss-Jordan elimination**, which consists in writing $$\mat{A}$$ and $$\mat{I}$$ side-by-side and conducting identical row operations on both to reduce $$\mat{A}$$ to $$\mat{I}$$. If this procedure can be completed successfully, then the companion array that started out as $$\mat{I}$$ will have been reduced to $$\mat{A}^{-1}$$. *Row operations* consist in multiplying a row by a scalar value and adding it to another row. The procedure is easiest to understand with an example.

We seek to invert the matrix
\\\[
  \mat{A} = \begin{pmatrix}
   1 & 2 & -3 \\\\ 
   2 & -1 & 4 \\\\ 
 -2 & 1 & 3 
 \end{pmatrix}
\\\]
so we write it next to the 3$$\times$$3 identity matrix:
\\\[
\begin{pmatrix}
1 & 2 & -3 & | & 1 & 0 & 0 \\\\ 
2 & -1 & 4 & | & 0 & 1 & 0 \\\\ 
-2 & 1 & 3 & | & 0 & 0 & 1
\end{pmatrix}
\\\]
To zero the first column of rows 2 and 3, we multiply the first row by $$-2$$ and 2, respectively, and add to get
\\\[
\begin{pmatrix}1 & 2 & -3 &  | &  1 & 0 & 0 \\\\ 
0 & -5 & 10 & | & -2 & 1 & 0 \\\\ 
0 & 5 & -3  & | &  2 & 0 & 1\end{pmatrix}
\\\]
Now divide the second row by $$-5$$ to get
\\\[
\begin{pmatrix}
1 & 2 & -3 &  | &  1 & 0 & 0 \\\\ 
0 & 1 & -2 & | & 2/5 & -1/5 & 0 \\\\ 
0 & 5 & -3  & | &  2 & 0 & 1
\end{pmatrix}
\\\]
To eliminate the 5 on the second column of the third row, multiply the second row by $$-5$$ and add, giving
\\\[
\begin{pmatrix}1 & 2 & -3 & | &  1 & 0 & 0 \\\\ 
0 & 1 & -2 & | & 2/5 & -1/5 & 0 \\\\ 
0 & 0 &  7 & | & 0 & 1 & 1\end{pmatrix}
\\\]
Dividing the last row by 7 reduces the original matrix to standard upper-triangular form (ones on the main diagonal and zeros below it):
\\\[
\begin{pmatrix}
1 & 2 & -3 & | &  1 & 0 & 0 \\\\ 
0 & 1 & -2 & | & 2/5 & -1/5 & 0 \\\\ 
0 & 0 &  1 & | & 0 & 1/7 & 1/7
\end{pmatrix}
\\\]
Now we proceed from bottom to top, eliminating with row operations the nonzero entries above the main diagonal. Multiplying the final row by 2 and adding to the middle row gives
\\\[
\begin{pmatrix}
1 & 2 & -3 & | &  1 & 0 & 0 \\\\ 
0 & 1 &  0 & | & 2/5 & 3/35 & 2/7 \\\\ 
0 & 0 &  1 & | & 0 & 1/7 & 1/7
\end{pmatrix}
\\\]
We now add to the first row the second row multiplied by $$-2$$ and the third row multiplied by 3, which gives
\\\[
\begin{pmatrix}
1 & 0 & 0 & | &  1/5 & 9/35 & -1/7 \\\\ 
0 & 1 & 0 & | & 2/5 & 3/35 & 2/7 \\\\ 
0 & 0 & 1 & | & 0 & 1/7 & 1/7
\end{pmatrix}
\\\]
Thus, we have determined that 
\\\[
  \mat{A}^{-1} = \begin{pmatrix}
  \frac15 & \frac{9}{35} & -\frac17 \\\\ 
  \frac25 & \frac{3}{35} & \frac27 \\\\ 
  0       & \frac17      & \frac17
 \end{pmatrix}
\\\]
You may confirm that multiplying $$\mat{A}$$ by $$\mat{A}^{-1}$$ does indeed produce the identity matrix.
