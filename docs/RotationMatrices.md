# Rotation Matrices

The matrix 
\\[
  \mat{R}(\theta) = 
    \begin{pmatrix}
  \cos\theta & -\sin\theta \\\ 
  \sin\theta & \cos\theta
  \end{pmatrix}
\\]
rotates a column vector through angle $$\theta$$ in the counterclockwise direction. You can confirm that $$\mat{R}(\pi/2)$$ rotates $$\vu{x} \to \begin{pmatrix}1 \\\ 0\end{pmatrix}$$ into $$\vu{y} \to \begin{pmatrix} 0 \\\ 1 \end{pmatrix}$$ and $$\vu{y}$$ into $$-\vu{x}$$.

We can generalize readily to 3 dimensions, at least for rotations around one of the basis vectors. For example, 
\\[
    \begin{pmatrix}
    \cos\theta & 0 & \sin\theta \\\ 
    0 & 1 & 0 \\\ 
    -\sin\theta & 0 & \cos\theta
    \end{pmatrix}
\\]
rotates a column vector around the $$y$$ axis. All proper rotations (that don't alter the handedness of the basis vectors) have a determinant of 1. Improper rotations, which do change the handedness of the basis vectors, have determinant $$-1$$.

# Orthogonal Matrices

