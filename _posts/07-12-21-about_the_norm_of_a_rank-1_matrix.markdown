---
layout: post
title:  "About the Norm of Rank-1 Matrices"
date:   2021-07-12
categories: [Applied Linear Algebra]
---

François Role - Associate professor - Université de Paris

<francois.role@u-paris.fr>


---

What is the Frobenius norm of a rank-1 matrix made out of two unit vectors? And why is it worth asking the question!

Let's build a rank-1 matrix as the outer product of two unit vectors


```python
u = np.array([[1.], [2.], [5.]])
u = u / np.linalg.norm(u)
v = np.array([[3.], [4.], [2.]])
v = v / np.linalg.norm(v)
X = u @ v.T
X
```




    array([[0.10170953, 0.1356127 , 0.06780635],
           [0.20341905, 0.2712254 , 0.1356127 ],
           [0.50854763, 0.6780635 , 0.33903175]])



Using the most common definition of the Frobenius norm $‖.‖_𝐹$ 

$$
\begin{align}
\|X\|_F & =\sqrt{\sum_{i=1}^{m} \sum_{j=1}^{n} x_{i,j}^2 }=\sqrt{Tr(X^TX)}=\sqrt{Tr(XX^T)}\\
\end{align}
$$

We find that the norm of $X$ is $1$.


```python
print(np.linalg.norm(X, ord='fro', axis=None, keepdims=False) )
print(np.sqrt(np.trace(X @ X.T)))
print(np.sqrt(np.trace(X.T @ X)))
```

    1.0
    0.9999999999999999
    1.0


First of all, why is that? This is because:

