---
layout: post
title:  "Change of Basis, Diagonalization: a Completely Worked Out Numerical Example "
date:   2021-09-12
categories: [Applied Linear Algebra]
---

François Role - Associate professor - Université de Paris

<francois.role@u-paris.fr>


---


```python
import numpy as np
```

## 1. Given the matrix $A$ of a mapping, find a similar matrix $\tilde{A}$ which is easier to use

Let $A$ \begin{pmatrix}
2 & 1\\
1 & 2 
\end{pmatrix}

be the matrix of an endomorphism $T:R^2 \rightarrow R^2$, wrt the canonical basis $C$ of $R^2$ for both the domain and codomain.

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


Let $U = (\mathbf{u_1}, \mathbf{u_2})$ be the ordered basis of $R^2$ consisting of the eigenvectors of $A$. We choose as representatives of these eigenvectors $\mathbf{u_1}=\begin{pmatrix}
 1\\
1 \\
\end{pmatrix}$ and $\mathbf{u_2}=\begin{pmatrix}
 -1\\
1 \\
\end{pmatrix}$

The matrix 
$\big(\begin{smallmatrix}
1 & -1\\
1 & 1 \\
\end{smallmatrix}\big)$ is the representation of these basis vectors wrt the canonical basis $C$, and thus a change of basis matrix $P$ from $U$ to $C$.

For a vector represented in $U$ as 
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

So the passage matrix from $C$ to $U$ is $\begin{pmatrix}
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
    inverse of P : from C to B
     [[ 0.5  0.5]
     [-0.5  0.5]]


We are now in a position to compute the transformation matrix $\tilde{A}$ of the linear mapping $T$ wrt the new basis $U$:
$$
\tilde{A} = P^{-1}AP
$$


```python
A = np.matrix(A)
A_tilde = P_inv @ A @ P
A_tilde
```




    matrix([[3., 0.],
            [0., 1.]])



which is the diagonal matrix of the eigenvalues of $A$.
So it seems that to perform the transformation $T$ it is better to operate on points represented in $B$ using the matrix $\tilde{A}$ (wich is "similar" to $A$).

## 2. Given the matrix $A$ of a mapping, identify an equivalent matrix $\tilde{A}$ which is easier to use

Let  $A$ $\begin{pmatrix}
2 & 1\\
1 & 2 
\end{pmatrix}$ now be the matrix of an endomorphism $T_{B,C}:R^2 \rightarrow R^2$ where $B$ is the  basis
$\begin{pmatrix}
\frac{1}{2} & 0\\
0 & \frac{1}{2} \\
\end{pmatrix}$ and $C$ is the canonical basis of $R^2$.

We will seek the matrix $\tilde{A}$ of the mapping $T_{U,U}:R^2 \rightarrow R^2$

Compared to the previous case, the difficulty here is to compute the passage matrix from $U$ to $B$. We seek a matrix $S$ whose $i-th$ column $s_i$ is the coordinate representation of $u_i$ wrt $B$, that is $Bs_i=u_i$.

Given $U=$
$\big(\begin{smallmatrix}
1 & -1\\
1 & 1 \\
\end{smallmatrix}\big)$  and $B=$ 
$\begin{pmatrix}
\frac{1}{2} & 0\\
0 & \frac{1}{2} \\
\end{pmatrix}$ numpy tells us that the passage matrix from $U$ to $B$ is $S=$ $\big(\begin{smallmatrix}
2 & -2\\
2 & 2 
\end{smallmatrix}\big)$


the passage matrix from $C$ to $U$ is still $\begin{pmatrix}
\frac{1}{2} & \frac{1}{2}\\
-\frac{1}{2} &\frac{1}{2} \\
\end{pmatrix}$ which is $P^{-1}$.


```python
u_1 = np.array([1., 1.])
u_2 = np.array([-1., 1.])

B = np.array([[0.5, 0.],
              [0., 0.5]])

s_1 = np.linalg.solve(B, u_1)
s_2 = np.linalg.solve(B, u_2)

print(s_1, s_2)

S = np.hstack((s_1.reshape(2,1),s_2.reshape(2,1)))
S

```

    [2. 2.] [-2.  2.]





    array([[ 2., -2.],
           [ 2.,  2.]])



We are now in a position to compute the transformation matrix $\tilde{A}$ of the linear mapping $T_{B,C}$ wrt the new basis $U$:
$$
\tilde{A} = P^{-1}AS
$$

The transformation matrix $\tilde{A}$ is equivalent (not similar) to $A$ but still easier to us than $A$. 


```python
A = np.array([[2, 1],
              [1, 2]])
P = np.matrix([[1, -1],
               [1, 1]])
P_inv = P.I
A = np.matrix(A)
A_tilde = P_inv @ A @ S
A_tilde
```




    matrix([[6., 0.],
            [0., 2.]])


