---
layout: post
title:  "Shapley Values"
date:   2021-07-02 11:45:46 +0200
categories: [Interpretable Machine Learning]
---
## Making Explicit the Relationship between Two Common Formulations of the Shapley Value

François Role 
Associate professor - Université de Paris
<francois.role@u-paris.fr>
June 2021

---


Given a characteristic function $v$, a set $N$ of $n$ players, and $S$ a variable ranging over all coalitions of players not containing a player $i$, the Shapley value for $i$ is most often defined as:

\begin{equation}\label{v1}
\varphi_i(v) = \sum_{S \subseteq N \setminus \{i\}}\frac{|S|!(n-|S|-1)!}{n!} (v(S \cup \{i\}) - v(S))
\end{equation}

An intuition for this formula is as follows:  $|S|!$ denotes the number of ways in which the elements of $|S|$ can join the coalition before player $i$ while $(n-|S|-1)!$ is the number of ways members of $N \setminus S \cup \{i\}$ can join the coalition after player $i$. Thus, $|S|!(n-|S|-1)!$ represents the number of ways a certain coalition $S$ excluding $i$ can be formed, which is divided by the total number of permutations $n!$. $v(S \cup \{i\}) - v(S)$ represents the contribution of player $i$ when joining the coalition after all players in $S$.

An alternative common formula is:


\begin{equation}\label{v2}
\varphi_i(v) = \frac{1}{n} \sum_{S \subseteq N \setminus \{i\}} \binom{n-1}{|S|}^{-1}  (v(S \cup \{i\}) - v(S))
\end{equation}

The problem with equation (\ref{v2}) is that it obfuscates the notion of permutation. Our objective is to show how this new formulation relates to the former one.

First, we note that (\ref{v2}) can be rewritten as:

\begin{equation}\label{v3}
\varphi_i(v) = \frac{1}{n!} \sum_{S \subseteq N \setminus \{i\}} \binom{n-1}{|S|}^{-1} (n-1)! (v(S \cup \{i\}) - v(S))
\end{equation}

where the introduction of $(n-1)!$ makes reappear the notion of permutation which was not explicit in formula (\ref{v2}).


Expanding $\binom{n-1}{|S|}^{-1}$ and moving $n!$ into the sum, equation (\ref{v3}) can then be be rewritten so as to retrieve formula (\ref{v1}):


\begin{equation}\label{v4}
\begin{split}
&  \sum_{S \subseteq N \setminus \{i\}} \frac{|S|!(n-1)!}{(n-1)(n-2)\dots(n-|S|)n!} (v(S \cup \{i\}) - v(S)) \\
 = & \sum_{S \subseteq N \setminus \{i\}} \frac{|S|!(n-|S|-1)!}{n!} (v(S \cup \{i\}) - v(S))
\end{split}
\end{equation}



