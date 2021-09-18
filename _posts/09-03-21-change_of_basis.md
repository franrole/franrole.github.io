---
title: TITLE
mathjax: true
categories:
  - category
tags:
  - tag
---


# Change of Basis and Diagonalization: a Completely Worked Out Numerical Example 


```python
import numpy as np
```

Let $A$ \begin{pmatrix}
2 & 1\\
1 & 2 \\
\end{pmatrix}

be the matrix of an endomorphism $T:R^2 \rightarrow R^2$, using the standard basis of $R^2$.

The determinant of $A - \lambda I$ is $\lambda^2 - 4 \lambda + 3 = (\lambda -1)(\lambda-3)$, so $A$ has two distinct eigenvalues $1$ and $3$.


```python
A = np.array([[2, 1],[1, 2]])
A
```




    array([[2, 1],
           [1, 2]])




```python
eigenvalues, eigenvectors = np.linalg.eig(A)
print(eigenvalues)
```

    [3. 1.]


The eigenspace of $A$ associated with $1$ is the set of vectors

\begin{pmatrix}
x_1\\
x_2 \\
\end{pmatrix} 

such that 

\begin{cases}
2 x_1 + x_2  &=x_1 \\
x_1 + 2 x_2  &=x_2
\end{cases}

that is such that $x_1=-x_2$. The same kind of computation shows that the eigenspace associated with $3$ is the set of vectors such as $x_1=x_2$.

We can check that this indeed corresponds to the eigenvectors found by numpy.


```python
print(eigenvectors)
print(np.array_equal (A @ eigenvectors[:,0], 3. * eigenvectors[:,0]))
print(np.array_equal (A @ eigenvectors[:,1], 1. * eigenvectors[:,1]))
```

    [[ 0.70710678 -0.70710678]
     [ 0.70710678  0.70710678]]
    True
    True


Let $B = \{\mathbf{u_1}, \mathbf{u_2}\}$ be the basis of $R^2$ consisting of the eigenvectors of $A$. We choose as representatives of these eigenvectors $\mathbf{u_1}=$\begin{pmatrix}
 1\\
1 \\
\end{pmatrix} and $\mathbf{u_2}=$\begin{pmatrix}
 1\\
-1 \\
\end{pmatrix}

The matrix 
$\big(\begin{smallmatrix}
1 & -1\\
1 & 1 \\
\end{smallmatrix}\big)$ is the representation of these basis vectors wrt the canonical basis $C$, and thus a change of basis matrix $P$ from $B$ to $C$.

For a vector represented in $B$ as 
$\begin{pmatrix}
z_1\\
z_2 \\
\end{pmatrix}$ its representation $\begin{pmatrix}
x_1\\
x_2 \\
\end{pmatrix}$ in $C$ is obtained 
$\begin{pmatrix}
1 & -1\\
1 & 1 \\
\end{pmatrix}  \begin{pmatrix}
z_1\\
z_2 \\
\end{pmatrix}=\begin{pmatrix}
x_1\\
x_2 \\
\end{pmatrix} $ from which it can be derived that $\begin{cases}
z_1  &=\frac{1}{2}(x_1 + x_2)\\
z_2  &=\frac{1}{2}(x_2 -x_1)\\
\end{cases}$

So the passage matrix from $C$ to $B$ is $\begin{pmatrix}
\frac{1}{2} & \frac{1}{2}\\
-\frac{1}{2} &\frac{1}{2} \\
\end{pmatrix}$ which is $P^{-1}$.




```python
# The two changes of basis matrices
P = np.matrix([[1, -1],[1, 1]])
P_inv = P.I
print("P : from B to C\n", P)
print("inverse of P : from C to B\n",P_inv)
```

    P : from B to C
     [[ 1 -1]
     [ 1  1]]
    inverse of P : from C to C
     [[ 0.5  0.5]
     [-0.5  0.5]]



```python

```
