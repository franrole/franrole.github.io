---
layout: post
title:  "Some Basic but Useful Facts about Determinants"
date:   2021-07-10
categories: [Applied Linear Algebra]
---

François Role - Associate professor - Université de Paris

<francois.role@u-paris.fr>


---

In this post, I will review some basic but useful facts about determinants.



## Computing a determinant





For starters, let's compute the determinant of the following square matrix :

$$
\begin{bmatrix}
3 &4 &6 \\
0 &1 &2 \\
5& 3& 1 
\end{bmatrix}
$$





```python
import numpy as np
from numpy import linalg
A=np.mat("3 4 6 ; 0 1 2 ; 5 3 1")
```

The co-factor $A_{ij}$ of $A$ is $(-1)^{i+j}M_{ij}$ where $M_{ij}$ is the (minor) determinant of the submatrix derived from $A$ by removing line $i$ and column $j$.

Recall that $det A = \sum_{k=i}^{n}a_{ik} A_{ik}$ for any line $i$ (or any column $i$). We choose the 2nd line since it contains a $0$. The computation is as follows:

Compute $A_{22}$ as $(-1)^{2+2}(3-30)$


```python
A_22=(-1)**4 * (3-30) ; A_22
```




    -27



Compute $A_{23}$ as $(-1)^{2+3}(9-20)$


```python
A_23=(-1)**5 * (9-20) ; A_23
```




    11



$det A= a_{22}A_{22}  + a_{23}A_{23} = -27 + 2(11) =-5$

***NUMPY:*** verify the result using Numpy:


```python
linalg.det(A)
```




    -5.0000000000000036




```python
def cofactor(A,i,j) :
    submatrix=A[np.array(range(i)+range(i+1,A.shape[0]))[:,np.newaxis], range(j)+range(j+1,A.shape[1]) ]
    return (-1)**(i+j)  * linalg.det(submatrix)
    
detA= A[1,1] *  cofactor(A,1,1) + A[1,2] *  cofactor(A,1,2) ; detA


```

## Properties Of Determinants

### For two matrices $A$ and $B$ of the same order $det AB = det A \, det B$.


```python
A=np.matrix(np.random.randint(200, size=(4,4)));A
```




    matrix([[145, 128, 158,  23],
            [114,  59,   9,  85],
            [ 39, 104,  18,  74],
            [173,  75,  23,  59]])




```python
B=np.matrix(np.random.randint(200, size=(4,4)));B
```




    matrix([[140, 164, 153, 103],
            [119,  31,   6,  11],
            [ 50, 144,  24,  27],
            [ 62, 167,  41, 161]])




```python
linalg.det(A*B)
```




    -16342606685111668.0




```python
linalg.det(A) * linalg.det(B) 
```




    -16342606685111670.0

### If we form $B$ from a square matrix $A$ by adding a constant times one row of $A$ to another row of $A$ , then $det A =det B$.


```python
A = np.matrix([[143,  65, 129, 116],
        [ 18,  31,  37,  97],
        [124,  53, 101, 110],
        [195,  21,  98, 149]])

B= np.matrix([[143,  65, 129, 116],
        [ 161,  96,  166,  213],
        [124,  53, 101, 110],
        [195,  21,  98, 149]])

print(linalg.det(A))
print(linalg.det(B))

```

    -4830905.0
    -4830905.0


### $det A^T= det A$


```python
print(linalg.det(A.T))
```

    -4830905.0


### if $A$ is invertible $det A^{-1}= 1 /det A$


```python
print("{} = {}".format(linalg.det(A.I), 1./linalg.det(A)))
```

    -2.0700055165647044e-07 = -2.0700055165647044e-07


And most importantly, if a square $n \times n$ matrix $A$ has a $0$ determinant then:
- A is not invertible
- The columns are dependent
- The rows are dependent
- $Ax=b$ has no or infinitely many solutions
- $Ax=0$ has infinitely many solutions
- $A$ has $r<n$ pivots
- The reduced row echelon form has at least one zero row
- The column and row spaces have dimensions $r<n$
- $o$ is an eigenvalue of $A$
- $A^TA$ is only semi-definite
- $A$ has $r<n$ singular values

Let's check some of these properties using an example.

```python
A_sing = np.matrix([[143,  65],
        [ 286,  130]])

print("Two rows are dependent so we have det A = {} ".format(linalg.det(A_sing)))
print("The rank of  A is only {}".format(linalg.matrix_rank(A_sing)))
values = np.linalg.eig(A_sing)[0]
print(f"One of the eigenvalues of A is 0 ==>  {values}")
```

    Two rows are dependent so we have det A = 0.0 
    The rank of  A is only 1
    One of the eigenvalues of A is 0 ==>  [273.   0.]









