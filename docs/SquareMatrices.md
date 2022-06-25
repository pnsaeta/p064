# Square Matrices

Square matrices have a number of interesting properties and deserve special attention.

## Identity Matrix

The identity matrix has ones along the main diagonal and zeros everywhere else:
\begin{equation}
  \mat{I} = \begin{pmatrix}
    1 & 0 & 0 & \cdots & 0 \\\\\\ 
    0 & 1 & 0 & \cdots & 0 \\\\\\ 
    0 & 0 & 1 & \cdots & 0 \\\\\\ 
    \vdots & \vdots & \vdots & \ddots & \vdots \\\\\\ 
    0 & 0 & 0 & \cdots & 1
    \end{pmatrix}
    \label{eq:identity}
\end{equation}

## Inverse

If a square matrix $$\mat{A}$$ has an inverse $$\mat{A}^{-1}$$, then
\begin{equation}
  \mat{A}^{-1} \mat{A} = \mat{I} = \mat{A} \mat{A}^{-1}
\end{equation}

If $$\mat{A}$$ transforms a column vector $$\vb{x}$$ to a new column vector $$\vb{y} = \mat{A}\vb{x}$$, the inverse matrix allows us to recover $$\vb{x}$$ from  $$\vb{y}$$ via $$\vb{x} = \mat{A}^{-1} \vb{y}$$ since
\begin{equation}
  \mat{A}^{-1} \vb{y} = \mat{A}^{-1} (\mat{A} \vb{x}) = (\mat{A}^{-1} \mat{A}) \vb{x} =  \mat{I} \vb{x} = \vb{x}
\end{equation}
The existence of an inverse implies that operating with $$\mat{A}$$ on a vector does not entail the loss of information; that is, the matrix lacks a **nullspace**, which means that its rows are linearly independent. It usually isn't obvious by inspection whether a square matrix has an inverse (that its rows are linearly independent). If one or more rows can be expressed as the linear combination of other rows, then the matrix is **singular**, its **determinant** vanishes, and it does not have an inverse.

You can use [Gauss-Jordan elimination](GaussJordan.md) to compute the inverse of a square matrix (provided it has one).
