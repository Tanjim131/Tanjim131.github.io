---
layout: post
title: Modular Multiplicative Inverse
subtitle: 
tags: [Number Theory]
comments: true
---

A modular multiplicative inverse of an integer $a$ is an integer $x$ such that,

\\[ a \cdot x \equiv 1 ~(\textrm{mod}~m) \\]

for some modulus $m \in \mathbb{Z}$. The above congruence can also be written as,

\\[ a \cdot a^{-1} \equiv 1 ~(\textrm{mod}~m) \\]

## <u> When does MMI exist ? </u>

The modular multiplicative inverse exists iff $a$ and $m$ are relatively prime, i.e., $\gcd(a,m) = 1$.

## <u> Computing MMI </u> <br> <br>
### 1. <u> Naive Implementation </u> 

We know that,

\\[ ax ~\textrm{mod}~m = ((a~\textrm{mod}~m) \cdot (x~\textrm{mod}~m))~\textrm{mod}~m\\]

$ x~\textrm{mod}~m $ will be any number between $0, 1, \cdots , m - 1$. So, we'll take numbers between $1,\cdots, m - 1$ one at a time, multiply that with $a~\textrm{mod}~m$ and check if the multiplication results in 1 modulo $m$.  

**Time Complexity**: $\mathcal{O}(m)$  

### 2. <u> Using Extended Euclidean Algorithm </u> 

From [Extended Euclidean Algorithm](./2020-05-19-extended-euclid.md), we know that the $\gcd(a,m)$ can be expressed in a linear equation,

\begin{equation}
    \label{MMIUEEA}
    a\cdot x + m\cdot y = \gcd(a,m) = 1
\end{equation}

where, $x,y \in \mathbb{Z}$. If we take $\textrm{modulo}~m$ on both sides of \eqref{MMIUEEA}, we'll have, 

\begin{equation}
    a \cdot x \equiv 1 ~\textrm{mod}~m
\end{equation}

So, $x$ is modular multiplicative inverse of $a~\textrm{mod}~m$.

In general, if $a$ and $b$ are co-prime, then from the following equation,

\\[ a\cdot x + b\cdot y = \gcd(a,b) = 1\\]

$x$ is the modular multiplicative inverse of $a~\textrm{mod}~b$ and $y$ is the modular multiplicative inverse of $b~\textrm{mod}~a$. Either $x$ or $y$ will be negative in this case.  

**Time Complexity**: Generally more efficient than [Exponentiation By Squaring](./2020-05-19-exponentiation-by-squaring.md).

\\[ \mathcal{O}(\log~(m)^{2})~\textrm{(Recursive, Two-pass)} \\]
\\[ \mathcal{O}(\log~m)~\textrm{(Iterative, One-pass)} \\] 


**Demonstration**: Let $a = 84$ and $b = 23$, then $\gcd(a,b) = \gcd(84,23) = 1$ and they can be expressed as,

\\[ 84\cdot(-3) + 23\cdot11 = 1\\]

Therefore, $x = -3$ and $y = 11$.

For ease of calculation positive remainder is used. 

Therefore, $x = (-3)~\textrm{mod}~23 = (-3) + 23 = 20$.

We can verify that the co-efficients are indeed correct. 

\\[ ax \equiv 1 ~\textrm{mod}~b \\]
\\[ \Rightarrow 84 \cdot 20 \equiv 1~\textrm{mod}~23\\]

And,

\\[ by \equiv 1 ~\textrm{mod}~a \\]
\\[ \Rightarrow 23 \cdot 11 \equiv 1~\textrm{mod}~84\\]

<!-- <li> <h3> <u> Using Euler's Totient Function </u> </h3> </li>

Will update later -->

### 3. <u> Using Fermat's Little Theorem </u>

See [Fermat's Little Theorem](./2020-05-19-fermats-little-theorem.md).