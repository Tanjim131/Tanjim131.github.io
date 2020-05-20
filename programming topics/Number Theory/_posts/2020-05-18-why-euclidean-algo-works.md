---
layout: post
title: Why does the Euclidean Algorithm for finding G.C.D of two number work?
subtitle: A look into the inner workings of the Euclidean Algorithm
tags: [Number Theory]
comments: true
---

We can prove that the Euclidean Algorithm works by using a standard argument in number theory: showing that a problem is equivalent to the same problem for smaller numbers.

Start with two numbers $a > b \geq 0$. You want to know two things:


1. Their greatest common divisor $g$,
2. and how to represent $g$ as a combination of $a$ and $b$

When, $b = 0$, $\gcd(a,b) = \gcd(a,0) = a$.

Suppose $ b > 0 $. Then, 

\begin{equation}
\label{WEAW1}
a = qb + r
\end{equation}

where $q$ is the quotient and $r = a~\textrm{mod}~b$ is the remainder.

From [Bezout's Identity](./2020-05-19-bezouts-identity.md), we know that $g$ can be expressed as a linear combination of $a$ and $b$. Namely, for $x,y \in \mathbb{Z}$ we have,

\begin{equation}
    \label{WEAW2}
    a \cdot x + b \cdot y = g
\end{equation}

We'll prove that $\gcd(a,b) = \gcd(b,r)$. There are two cases:


1. $g \mid a$ and $g \mid b$. So, from \eqref{WEAW1}, $g \mid r$. Therefore, $g \mid \gcd(b,r) $. 
( [See Lemma 1](#lemma-1) )
2. Let $c = \gcd(b,r)$. From \eqref{WEAW1}, $c \mid b$ and $c \mid r$. So, from \eqref{WEAW1}, $c \mid a$.   
Therefore, $c \mid \gcd(a,b)$.


From [Lemma 2](#lemma-2), we have $g = c$ or $\gcd(a,b) = \gcd(b,r)$.

**Alternate proof by contradiction**: Let's assume $g > c$. We know $g \mid b,r$. So we have a number $g$ which is greater than $c$ and divides both $b$ and $r$. This implies $c \not= \gcd(b,r)$. But we know, $c = \gcd(b,r)$. So, $g \not> c$. Similar reasoning can be shown in case of $g < c$. Therefore we conclude, $g = c$.

Moreover, if you can write $g$ as a combination of $b$ and $r$, then you can write it as a combination of $a$ and $b$ (substitute in \eqref{WEAW1}). That means if you can solve \eqref{WEAW2} for the pair $(b,r)$ then you can solve it for the pair $(a,b)$.

Taken together, this argument shows that you can replace your problem for $(a,b)$ by the same problem for the smaller pair $(b,r)$. Since the problem can't keep getting smaller forever, eventually you will reach $(z,0)$ and you're done. &nbsp; $ \blacksquare $ 

**Time Complexity**: $\mathcal{O}(\lg a) = \mathcal{O}(\lg a + \lg b) = \mathcal{O}(5\log_{10}b)$

Where, $a \geq b$ and the complexity is given in the number of division steps.  
( Source: [The Art of Computer Programming : Volume 2](https://dl.acm.org/doi/book/10.5555/270146) )

#### ***Lemma 1***
$c \mid a, b  \Longleftrightarrow c \mid d $ for $d = \ddfrac{ab}{\lcm{(a,b)}}$. Hence $ d = \gcd(a,b) $.  
***Proof***: $c \mid a, b  \Longleftrightarrow a,b \mid \ddfrac{ab}{c} \Longleftrightarrow \lcm{(a,b)} \mid \ddfrac{ab}{c} \Longleftrightarrow c \mid \ddfrac{ab}{\lcm{(a,b)}}$ 

### ***Lemma 2***
If $a \mid b$ and $b \mid a$, then $a = \pm b$.

***Proof***: As, $a \mid b$, we have,
\begin{equation}
    \label{EAL1EQ1}
    p \cdot a = b 
\end{equation}
for some $p \in \mathbb{Z}$. Similarly, 
\begin{equation}
    \label{EAL1EQ2}
    q \cdot b = a 
\end{equation}
for some $q \in \mathbb{Z}$. Replacing $a$ from \eqref{EAL1EQ2} in \eqref{EAL1EQ1}, we have,
\begin{equation}
    \label{EAL1EQ3}
    p \cdot (q \cdot b) = b 
\end{equation}
As $ b \not= 0$, we divide both sides of \eqref{EAL1EQ3} to get,
\begin{equation}
    p \cdot q = 1
\end{equation}

As, $p$ and $q$ are both integers, we have only two solutions. Either $(p,q) = (1,1)$ or $(p,q) = (-1,-1)$. For $(p,q) = 1$ we have, $a = b$ and 
for $(p,q) = (-1,-1)$ we have, $a = -b$. So, $ a = \pm b$. &nbsp; $\blacksquare$

***Sidenote***: Although we have $a > b \geq 0$ in our reasoning, if any or both them are negative numbers, it won't effect our $\gcd$ calculation. Because we have,


\\[ \gcd(a,b) = \gcd(\abs{a},b) = \gcd(a,\abs{b}) = \gcd(\abs{a},\abs{b}) \\]
