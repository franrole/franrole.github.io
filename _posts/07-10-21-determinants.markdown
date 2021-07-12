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



