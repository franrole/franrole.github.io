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
