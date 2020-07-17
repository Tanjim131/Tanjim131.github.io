---
layout: post
title: Number of digits from $1$ to $n$
tags: [Combinatorics]
---

Let $n$ be a natural number comprising $k$ digits. We know that a number $n$ has exactly $\floor{\log_{b}(k)} + 1$ digits in base $b$ <sup> [[Source]](https://math.stackexchange.com/a/335063/529269) </sup>. So, in base $10$, $n$ has exactly $k = \floor{\log_{10}(n)} + 1$ digits. 

Let $d(n)$ be the number of digits required to write the natural numbers from $1$ to $n$. For example $d(12) = 15$ because we need $15$ digits to write down the numbers from $1$ to $12$. We have to show that,

\begin{eqnarray}
d(n) = k(n + 1) - \underbrace{111\ldots111}_{k~\textrm{digits}} = k(n + 1) - \ddfrac{10^{k} - 1}{9}
\end{eqnarray}

***Proof***: 