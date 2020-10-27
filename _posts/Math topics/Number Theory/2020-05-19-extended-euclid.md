---
layout: post
title: Extended Euclidean Algorithm
subtitle: 
tags: [Number Theory]
comments: true
---

For two integers, $a$ and $b$, extended euclidean algorithm computes $\gcd(a,b)$ and coefficients $x,y \in \mathbb{Z}$ such that,

\\[ ax + by = \gcd(a,b) \\]

From [Bezout's Identity](./2020-05-19-bezouts-identity.md), we know that a solution to this equation exists.

Let, $\gcd(a,b) = g$. When, $(a,b) = (g,0)$, the equation has a trivial solution, $(x,y) = (1,0)$. We get this value when we follow the computation trail of the normal euclidean algorithm. We can then backtrack recursively to get the $(x,y)$ pair for the original $(a,b)$ pair.

Remember the recursive computation of normal euclidean algorithm? We go from $(a,b)$ to $(b, a ~\textrm{mod}~b)$ until we reach $(a ~\textrm{mod}~ b) = 0$.

Let's assume for any $(b, a ~\textrm{mod}~b)$, we found the coefficients $(x_1, y_1)$ such that,

\begin{equation}
    \label{EEA1}
    b \cdot x_1 +  (a ~\textrm{mod}~b) \cdot y_1 = g
\end{equation}

and we want to find pair $(x,y)$ such that,

\\[ a\cdot x + b\cdot y = g\\]

$a ~\textrm{mod}~b$ can be written as, 

\\[ a ~\textrm{mod}~b = a - \floor{\frac{a}{b}} \cdot b \\]

Substituting this expression in \eqref{EEA1} we get,

\begin{equation}
    \label{EEA2}
    g = b \cdot x_1 + (a - \floor{\frac{a}{b}} \cdot b) \cdot y1
\end{equation}

After rearranging terms in (\ref{EEA2}) we'll get,

\\[ g = a \cdot y_1 + b\cdot(x_1 - y_1\cdot\floor{\frac{a}{b}})\\]

And so,

\begin{aligned}
x & = y_1 \newline
y & = x_1 - y_1\cdot\floor{\frac{a}{b}} \newline
\end{aligned}
