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

Let's build a rank-1 matrix as the outer product of two unit vectors $\|\|F\|\| = \sqrt{\sum_{k=1}^2}$.


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
    0.999
    1.0


First of all, why is that? This is because:

$$
\|X\|_F =\|uv^T\|_F = \sqrt{tr(uv^Tvu^T)} = \sqrt{tr(uu^T)} = \sqrt{tr(u^Tu)} = \sqrt{1}=1
$$

And now, what's the point of investigating this?
Because this fact allows to derive another definition for the Frobenius norm. 

Given a SVD decomposition  $X = \sum_{k=1}^{r} \sigma_ku_kv_k^T$, we have:

$$
\|X\|_F = \|\sum_{k=1}^{r} \sigma_ku_kv_k^T \|_F= \sqrt{\sum_{k=1}^{r}  \sigma_k^2\| u_kv_k^T \|_F}= \sqrt{\sum_{k=1}^{r}  \sigma_k^2}
$$

where in addition to $\|\| u_kv_k^T \|\|_F=1$ we also use the fact that the norm of a (weighted sum of matrix can be expressed in terms of the norms of the individual matrices:

$$
\|\sum_{i=1}^{n}  \alpha_i  X_i \|_F^2 = \sum_{i=1}^{n}  \alpha_i^2 \| A_i \|_F^2
$$

Note that the result $\|\|X\|\|_F =  \sqrt{\sum_{k=1}}$ is more commonly derived as:

$$
\|U\Sigma V^T\|_F = \sqrt{trace(U\Sigma V^T V\Sigma U^T)}= \sqrt{trace(U\Sigma \Sigma U^T)}= \sqrt{trace(\Sigma U^T U\Sigma)}=\sqrt{trace(\Sigma^2)}
$$





