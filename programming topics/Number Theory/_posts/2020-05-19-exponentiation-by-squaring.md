---
layout: post
title: Exponentiation By Squaring
subtitle: Finding $ a^{n}~\rm{mod}~m $ in $ \mathcal{O}(\lg~n) $ time
tags: [Number Theory]
comments: true
---

Given a base $a$, an exponent $n$ and a mod $m$, we have to compute $a^n ~\textrm{mod}~m$. 

## <u> Naive Approach </u>

Loop $ n - 1 $ times to get $a^n$. In each step, perform multiplication and modulo operation, i.e., $(a \cdot a)~\textrm{mod}~m$. Impractical for large $a$ or $n$.

**Time Complexity**: $\mathcal{O}(n)$

## <u> Efficient Approach </u>

We make use of the binary representation of the exponent ($n$). 

We know that, a number $n$ has exactly $ \floor{\log_{2}(n)} + 1$ digits in base $2$.

So, we need to perform at most $\mathcal{O}(\log n)$ multiplications, given that we know the powers $a^1, a^2, a^4, \cdots , a^{\floor{\log_2(n)}}$. 

Expressed recursively,

\\[
a^n =  
\begin{cases}
  1 & \textrm{if $ n == 0 $} \\\
  (a^{\sfrac{n}{2}})^2 & \textrm{if $n$ is even} \\\
  (a^{\sfrac{n - 1}{2}})^2 \cdot a & \textrm{if $n$ is odd}
\end{cases}
\\]


**Time Complexity**: $\mathcal{O}(\lg~n)$
