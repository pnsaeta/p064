{:menu LinAl}
{::comment}menu-start{:/comment}

<div class="dropdown">
<label id="hamburger-menu"><img id="hamburger" src="figs/hamburger.png"></label>
<div class="dropdown-content">
<ul>
<li><a href="LinearAlgebra.html">Linear Algebra</a></li>
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
You may confirm that multiplying $$\mat{A}$$ by $$\mat{A}^{-1}$$ does indeed produce the identity matrix. Here's how to make Python do it:

~~~~ python
import numpy as np

mat = np.array([[1,2,-3],[2,-1,4],[-2,1,3]])
inv = np.array([[1/5, 9/35, -1/7],[2/5, 3/35, 2/7],[0,1/7,1/7]])
mat @ inv

array([[1.00000000e+00, 0.00000000e+00, 0.00000000e+00],
       [0.00000000e+00, 1.00000000e+00, 0.00000000e+00],
       [0.00000000e+00, 5.55111512e-17, 1.00000000e+00]])
~~~~

Up to numerical round-off error, we do indeed get the identity matrix.

## LU Decomposition

The procedure just outlined uses a sequence of pivots to reduce the input matrix $$\mat{A}$$ to upper-triangular form (all entries below the main diagonal get sent to zero). In general, we will need to resort to permuting some rows to avoid zero pivots, so we will assume that we can 
factor $$\mat{P}\vdot\mat{A} = \mat{L}\vdot\mat{U}$$. In that case, the task of solving the equation
\\[
  \mat{P}\vdot\mat{A}\vdot\vb{x} = \mat{L} \vdot \mat{U} \vdot\vb{x} = \mat{P}\vdot \vb{b}
\\]
for $$\vb{x}$$ can be decomposed into two straightforward problems. We first solve
\\[
  \mat{L}\vdot\vb{y} = \mat{P}\vdot\vb{b}
\\]
for $$\vb{y}$$ and then solve
\\[
  \mat{U}\vdot\vb{x} = \vb{y}
\\]
for $$\vb{x}$$. Because the former can be solved by forward substitution and the latter by backward substitution, each subproblem is solved efficiently and if we have to solve for several different right-hand sides $$\vb{b}$$, we only need to do the LU decomposition once to realize the efficiency gains for all.

### Permutation Matrices

A **permutation matrix** is a version of the identity matrix in which the rows (columns) have been shuffled in some fashion. Suppose that we need to exchange rows 2 and 3 of a 3-dimensional matrix to avoid a zero pivot. The matrix that accomplishes this is
\\[
  \mat{P}_{23} = \begin{pmatrix}
  1 & 0 & 0 \\\ 0 & 0 & 1 \\\ 0 & 1 & 0
  \end{pmatrix}
\\]
It simply has rows 2 and 3 of an identity matrix exchanged. Note that the determinant of a permutation matrix flips sign for each pair of rows exchanged, so the determinant of $$\mat{P}_{23} = -1$$.

### Elementary Matrices

As we perform the steps of Gauss-Jordan elimination, we multiply an earlier row $$j$$ by a coefficient $$c_{ij}$$ and add it to a later row $$i > j$$, in order to set to zero entry $$ij$$ of the matrix. For example, in the above example, the first step of elimination was to multiply the first row by $$c_{21} = -2$$ and add it to the second row. The **elementary matrix** that accomplishes this operation is
\\[
  \mat{E}_{12} = \begin{pmatrix}
  1 & 0 & 0 \\\ -2 & 1 & 0 \\\ 0 & 0 & 1
  \end{pmatrix}
\\]
which differs from the identity matrix by the single off-diagonal element $$-2$$ in row 2, column 1. You can verify that if we multiply $$\mat{A}$$ by $$\mat{E}_{12}$$, the result is to add $$-2$$ times row 1 to row 2 and to leave rows 1 and 3 unchanged.

The next operation we needed was to multiply row 1 by $$c_{31} = 2$$ and add it to row 3, which we could accomplish with
\\[
  \mat{E}\_{13} = \begin{pmatrix}
  1 & 0 & 0 \\\ 0 & 1 & 0 \\\ 2 & 0 & 1
  \end{pmatrix}
\\]
So far, therefore, we have transformed $$\mat{A}$$ first by multiplying by $$\mat{E}_{12}$$ and then by $$\mat{E}_{13}$$ to get
\\[
  \mat{E}\_{13} \vdot \mat{E}\_{12} \vdot \mat{A} = 
  \begin{pmatrix}
    1 & 2 & -3 \\\ 0 & -5 & 10 \\\ 0 & 5 & -3
  \end{pmatrix}
\\]
The final elementary matrix we need to reduce $$\mat{A}$$ to upper-triangular form has $$c_{32} = 1$$ and is therefore
\\[
  \mat{E}_{23} = \begin{pmatrix}
  1 & 0 & 0 \\\ 0 & 1 & 0 \\\ 0 & 1 & 1
  \end{pmatrix}
\\]


### From $$\mat{U}$$ to $$\mat{L}$$

We have now found that by applying the three elementary matrices in the appropriate order,
we can reduce $$\mat{A}$$ to upper-triangular form:
\\[
  \mat{E}\_{23} \vdot \mat{E}\_{13} \vdot \mat{E}\_{12} \vdot \mat{A}
  =
  \begin{pmatrix}
  1 & 2 & -3 \\\ 0 & -5 & 10 \\\ 0 & 0 & 7
  \end{pmatrix}
  = \mat{U}
\\]
If we were now to successively apply inverse elementary matrices from the left, we could recover $$\mat{A}$$ while simultaneously constructing $$\mat{L}$$ on the right:
\\[
  \mat{L} = \mat{E}\_{12}^{-1} \vdot \mat{E}\_{13}^{-1} \vdot \mat{E}\_{23}^{-1}
  \qqtext{so that}
  \mat{A} = \mat{L}\vdot\mat{U}
\\]

What would the inverse of $$\mat{E}\_{23}$$ look like? Well, $$\mat{E}\_{23}$$ multiplies row 2 by 1 and adds it to row 3. Undoing this procedure would multiply row 2 by $$-1$$ and add it to row 3:
\\[
  \mat{E}\_{23}^{-1} = \begin{pmatrix}
    1 & 0 & 0 \\\ 0 & 1 & 0 \\\ 0 & -1 & 1
  \end{pmatrix}
\\]
So, we have
\\[
  \mat{L} = 
  \underbrace{\begin{pmatrix}
    1 & 0 & 0 \\\ 2 & 1 & 0 \\\ 0 & 0 & 1
   \end{pmatrix}}\_{\mat{E}\_{12}^{-1}}
  \vdot
  \underbrace{\begin{pmatrix}
    1 & 0 & 0 \\\ 0 & 1 & 0 \\\ -2 & 0 & 1
   \end{pmatrix}}\_{\mat{E}\_{13}^{-1}}
  \vdot
  \underbrace{\begin{pmatrix}
    1 & 0 & 0 \\\ 0 & 1 & 0 \\\ 0 & -1 & 1
   \end{pmatrix}}\_{\mat{E}\_{23}^{-1}}
  =
  \begin{pmatrix}
    1 & 0 & 0 \\\ 2 & 1 & 0 \\\ -2 & -1 & 1
  \end{pmatrix}
\\]
Before going on to check that multiplying this matrix on the right by $$\mat{U}$$ produces $$\mat{A}$$, notice something amazing about its structure. In the final matrix, the elements below the main diagonal are just the negatives of the coefficients $$c_{ij}$$ that we found in the process of reducing $$\mat{A}$$ to upper-diagonal form. The form of the elementary matrices and the order in which we multiply them to generate $$\mat{L}$$ allows us to simply write down the form of $$\mat{L}$$ directly from the coefficients $$c_{ij}$$!

### Check

If all is well, when we multiply $$\mat{L}$$ by $$\mat{U}$$, we should get $$\mat{A}$$:
\\[
  \begin{pmatrix}
    1 & 0 & 0 \\\ 2 & 1 & 0 \\\ -2 & -1 & 1
  \end{pmatrix} \vdot
  \begin{pmatrix}
  1 & 2 & -3 \\\ 0 & -5 & 10 \\\ 0 & 0 & 7
  \end{pmatrix}
  = \begin{pmatrix}
  1 & 2 & -3 \\\ 2 & -1 & 4 \\\ -2 & 1 & 3
  \end{pmatrix}
\\]

~~~~ python
L = np.array([[1, 0, 0], [2, 1, 0], [-2, -1, 1]])
U = np.array([[1, 2, -3], [0, -5, 10], [0, 0, 7]])
L @ U
array([[ 1,  2, -3],
       [ 2, -1,  4],
       [-2,  1,  3]])
~~~~

which is indeed $$\mat{A}$$.

### Recap

So, Gaussian elimination entails progressively eliminating entries below the main diagonal by multiplying the pivot row by the necessary coefficient $$c_{ij}$$ and adding to the lower rows to set the column below the pivot to zeros. The lower-triangular matrix $$\mat{L}$$ is constructed starting with the identity matrix by filling in the coefficients $$-c_{ij}$$ below the main diagonal, while the upper-triangular matrix $$\mat{U}$$ results from applying the successive elimination steps to the original matrix $$\mat{A}$$.

## Numerical Approach

Gauss-Jordan elimination is straightforward to program. A naïve implementation would proceed just as I have in the example. However, especially as the **dimension** of the matrix to invert gets large, the method is numerically unstable and prone to round-off error. Fortunately, it isn't too hard to adjust the procedure to avoid this instability. The trick is called (partial) pivoting and involves exchanging rows to put the largest potential pivot in the pivot row. How does this work?

Let's start back at the beginning and scan the first column to look for the row whose first element has the greatest magnitude:
\\[
\begin{pmatrix}
1 & 2 & -3 & | & 1 & 0 & 0 \\\ 
2 & -1 & 4 & | & 0 & 1 & 0 \\\ 
-2 & 1 & 3 & | & 0 & 0 & 1
\end{pmatrix}
\\]
In this case, there is a tie between the second and third rows. I will pick row 2 and exchange rows 1 and 2 with the permutation matrix
\\[
  \mat{P} = \begin{pmatrix} 0 & 1 & 0 \\\ 1 & 0 & 0 \\\ 0 & 0 & 1 \end{pmatrix}
\\]
to get
\\[
\begin{pmatrix}
2 & -1 & 4 & | & 0 & 1 & 0 \\\ 
1 & 2 & -3 & | & 1 & 0 & 0 \\\ 
-2 & 1 & 3 & | & 0 & 0 & 1
\end{pmatrix}
\\]

Multiplying the first row by $$c_{21} = -1/2$$ and adding to the second row, followed by multiplying the first row by $$c_{31} = 1$$ and adding to the third row gives
\begin{equation}\label{eq:halfway}
\begin{pmatrix}
2 & -1  & 4 &  | & 0 & 1    & 0 \\\ 
0 & 5/2 & -5 & | & 1 & -1/2 & 0 \\\ 
0 & 0    & 7 & | & 0 & 1    & 1
\end{pmatrix}
\end{equation}

Before proceeding to the inverse, we have managed the LU decomposition of the matrix $$\mat{P}\vdot\mat{A}$$ as
\begin{equation}\label{eq:LU}
  \mat{P} \vdot \mat{A} =
  \underbrace{\begin{pmatrix}
  1 & 0 & 0 \\\ 1/2 & 1 & 0 \\\ -1 & 0 & 1
  \end{pmatrix}}\_{\mat{L}}
  \vdot
  \underbrace{\begin{pmatrix}
  2 & -1 & 4 \\\ 0 & 5/2 & -5 \\\ 0 & 0 & 7  
  \end{pmatrix}}\_{\mat{U}}
\end{equation}

### LDU Decomposition

Before finishing Gauss-Jordan elimination, I'd like to adjust $$\mat{U}$$ to have ones along the main diagonal. We can accomplish this normalization by dividing each row by its pivot and collecting those divisors along the main diagonal of a matrix $$\mat{D}$$,
\\[
  \mat{U} = \underbrace{\begin{pmatrix}
  2 & 0 & 0 \\\ 0 & \frac52 & 0 \\\ 0 & 0 & 7
  \end{pmatrix}}\_{\mat{D}} \vdot
  \underbrace{\begin{pmatrix}
  1 & -\frac12 & 2 \\\ 0 & 1 & -\frac{10}3 \\\ 0 & 0 & 1
  \end{pmatrix}}_{\mat{U'}}
\\]
so that the matrix $$\mat{P}\vdot\mat{A}$$ is now expressed
\\[
  \mat{P}\vdot\mat{A} = \mat{L} \vdot \mat{D} \vdot \mat{U}'
  = \begin{pmatrix}
    1 & 0 & 0 \\\ 2 & 1 & 0 \\\ -2 & -1 & 1
  \end{pmatrix} \vdot \begin{pmatrix}
  2 & 0 & 0 \\\ 0 & \frac52 & 0 \\\ 0 & 0 & 7
  \end{pmatrix} \vdot
  \begin{pmatrix}
  1 & -\frac12 & 2 \\\ 0 & 1 & -\frac{10}{3} \\\ 0 & 0 & 1
  \end{pmatrix}
\\]
Notice that the determinants of the two triangular matrices are 1; the determinant of $$\mat{P}\vdot\mat{A}$$ is thus the determinant of $$\mat{D}$$, which is the product of its nonzero (diagonal) elements.

~~~~ python
>>> import numpy as np
>>> from scipy.linalg import lu
>>> A = np.array([[1,2,-3],[2,-1,4],[-2,1,3]])
>>> A
array([[ 1,  2, -3],
       [ 2, -1,  4],
       [-2,  1,  3]])
>>> P, L, U = lu(A)
>>> P
array([[0., 1., 0.],
       [1., 0., 0.],
       [0., 0., 1.]])
>>> L
array([[ 1. ,  0. ,  0. ],
       [ 0.5,  1. ,  0. ],
       [-1. ,  0. ,  1. ]])
>>> U       
array([[ 2. , -1. ,  4. ],
       [ 0. ,  2.5, -5. ],
       [ 0. ,  0. ,  7. ]])
~~~~

The `lu` function of `scipy.linalg` returns the three matrices $$\mat{P}$$, $$\mat{L}$$, and $$\mat{U}$$, getting just what we did from the straight LU decomposition of $$\mat{A}$$.

If we want a complete LDU factorization, we can pull the values of $$\mat{D}$$ from the diagonal of $$\mat{U}$$ and divide the rows of $$\mat{U}$$ by these values:

~~~~ python
>>> D = np.diag(np.diag(U))
>>> D
array([[2. , 0. , 0. ],
       [0. , 2.5, 0. ],
       [0. , 0. , 7. ]])
>>> U /= np.diag(U)
>>> U
array([[ 1.        , -0.4       ,  0.57142857],
       [ 0.        ,  1.        , -0.71428571],
       [ 0.        ,  0.        ,  1.        ]])
~~~~

### Finishing up

Let's now return to Eq. (\ref{eq:halfway}) to finish computing the inverse.
Multiply the second row by $$2/5$$ (and the final row by $$1/7$$):
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
which yields the same result for the inverse as before. Even having permuted the first and second rows to use the largest available pivot, *we get the same inverse matrix*.
