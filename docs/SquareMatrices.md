# Square Matrices

Square matrices have a number of interesting properties and deserve special attention.

## Identity Matrix

The identity matrix has ones along the main diagonal and zeros everywhere else:
\begin{equation}
  \mathbb{I} = \begin{pmatrix}
    1 & 0 & 0 & \cdots & 0 \\\ 0 & 1 & 0 & \cdots & 0 \\\ 0 & 0 & 1 & \cdots & 0 \\\ \vdots & \vdots & \vdots & \ddots & \vdots \\\ 0 & 0 & 0 & \cdots & 1
    \end{pmatrix}
    \label{eq:identity}
\end{equation}

## Inverse

If a square matrix $$\mathbb{A}$$ has an inverse $$\mathbb{A}^{-1}$$, then
\begin{equation}
  \mathbb{A}^{-1} \mathbb{A} = \mathbb{I} = \mathbb{A} \mathbb{A}^{-1}
\end{equation}

If $$\mathbb{A}$$ transforms a column vector $$\vb{x}$$ to a new column vector $$\vb{y} = \mathbb{A}\vb{x}$$, the inverse matrix allows us to recover $$\vb{x}$$ from  $$\vb{y}$$ via $$\vb{x} = \mathbb{A}^{-1} \vb{y}$$ since
\begin{equation}
  \mathbb{A}^{-1} \vb{y} = \mathbb{A}^{-1} (\mathbb{A} \vb{x}) = (\mathbb{A}^{-1} \mathbb{A}) \vb{x} =  \mathbb{I} \vb{x} = \vb{x}
\end{equation}
The existence of an inverse implies that operating with $$\mathbb{A}$$ on a vector does not entail the loss of information; that is, the matrix lacks a **nullspace**, which means that its rows are linearly independent. It usually isn't obvious by inspection whether a square matrix has an inverse (that its rows are linearly independent). If one or more rows can be expressed as the linear combination of other rows, then the matrix is **singular**, its **determinant** vanishes, and it does not have an inverse.

One can seek the inverse of a given square matrix $$\mathbb{A}$$ using **Gauss-Jordan elimination**, which consists in writing $$\mathbb{A}$$ and $$\mathbb{I}$$ side-by-side and conducting identical row operations on both to reduce $$\mathbb{A}$$ to $$\mathbb{I}$$. If this procedure can be completed successfully, then the companion array that started out as $$\mathbb{I}$$ will have been reduced to $$\mathbb{A}^{-1}$$. *Row operations* consist in multiplying a row by a scalar value and adding it to another row. The procedure is easiest to understand with an example.

We seek to invert the matrix
\[
  \mathbb{A} = \begin{pmatrix} 1 & 2 & -3 \\\ 2 & -1 & 4 \\\ -2 & 1 & 3 \end{pmatrix}
\]
so we write it next to the 3$$\times$$3 identity matrix:
\[
\begin{pmatrix}
1 & 2 & -3 & | & 1 & 0 & 0 \\\
2 & -1 & 4 & | & 0 & 1 & 0 \\\
-2 & 1 & 3 & | & 0 & 0 & 1
\end{pmatrix}
\]
To zero the first column of rows 2 and 3, we multiply the first row by $$-2$$ and 2, respectively, and add to get
\[
\begin{pmatrix}
1 & 2 & -3 &  | &  1 & 0 & 0 \\\
0 & -5 & 10 & | & -2 & 1 & 0 \\\
0 & 5 & -3  & | &  2 & 0 & 1
\end{pmatrix}
\]
Now divide the second row by $$-5$$ to get
\[
\begin{pmatrix}
1 & 2 & -3 &  | &  1 & 0 & 0 \\\
0 & 1 & -2 & | & 2/5 & -1/5 & 0 \\\
0 & 5 & -3  & | &  2 & 0 & 1
\end{pmatrix}
\]
To eliminate the 5 on the second column of the third row, multiply the second row by $$-5$$ and add, giving
\[
\begin{pmatrix}
1 & 2 & -3 & | &  1 & 0 & 0 \\\
0 & 1 & -2 & | & 2/5 & -1/5 & 0 \\\
0 & 0 &  7 & | & 0 & 1 & 1
\end{pmatrix}
\]
Dividing the last row by 7 reduces the original matrix to standard upper-triangular form (ones on the main diagonal and zeros below it):
\[
\begin{pmatrix}
1 & 2 & -3 & | &  1 & 0 & 0 \\\
0 & 1 & -2 & | & 2/5 & -1/5 & 0 \\\
0 & 0 &  1 & | & 0 & 1/7 & 1/7
\end{pmatrix}
\]
Now we proceed from bottom to top, eliminating with row operations the nonzero entries above the main diagonal. Multiplying the final row by 2 and adding to the middle row gives
\[
\begin{pmatrix}
1 & 2 & -3 & | &  1 & 0 & 0 \\\
0 & 1 &  0 & | & 2/5 & 3/35 & 2/7 \\\
0 & 0 &  1 & | & 0 & 1/7 & 1/7
\end{pmatrix}
\]
We now add to the first row the second row multiplied by $$-2$$ and the third row multiplied by 3, which gives
\[
\begin{pmatrix}
1 & 0 & 0 & | &  1/5 & 9/35 & -1/7 \\\
0 & 1 & 0 & | & 2/5 & 3/35 & 2/7 \\\
0 & 0 & 1 & | & 0 & 1/7 & 1/7
\end{pmatrix}
\]
Thus, we have determined that 
\[
  \mathbb{A}^{-1} = \begin{pmatrix}
 \frac15 & \frac{9}{35} & -\frac17 \\\
 \frac25 & \frac{3}{35} & \frac27 \\\
 0       & \frac17      & \frac17
 \end{pmatrix}
\]
You may confirm that multiplying $$\mathbb{A}$$ by $$\mathbb{A}^{-1}$$ does indeed produce the identity matrix.

