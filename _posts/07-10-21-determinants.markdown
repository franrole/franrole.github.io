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


# Determinants 

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






