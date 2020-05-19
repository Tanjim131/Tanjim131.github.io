---
layout: post
title: Linear Congruence
subtitle: 
tags: [Number Theory]
comments: true
---

<h2> <u> When can you divide a congruence? </u> </h2>

You can divide both sides of a congruence relation when the number you’re diving and the mod are co-prime.

For example, you cannot divide the congruence $30 \equiv 42 (\textrm{mod}\ 4) $ by $6$ because $6$ and $4$ are not co-prime. (as $ \gcd (6,4) = 2 \not= 1 $).

<b> <i> Claim </i> </b>: If $ka \equiv kb ~ (\textrm{mod}\ n)$ and $ \gcd(k,n) = 1 $, then $ a \equiv b ~ (\textrm{mod}\ n)$.

<b> <i> Proof </i> </b>: As, $ka \equiv kb ~ (\textrm{mod}\ n)$, we have $n \mid k(a - b)$, but as $\gcd (k,n) = 1$, $n \nmid k$. So, we have, $n \mid (a - b)$. Therefore, $a \equiv b ~ (\textrm{mod}\ n)$. &nbsp; $ \blacksquare $ 

<h2> <u> Solving Linear Congruence </u> </h2>

We have to Solve,

\\[ 17x \equiv 3 ~ (\textrm{mod}\ 29) \\]

As, $17$ and $29$ are coprime, we can divide the congruence on both sides by $17$ to get,

\begin{equation}
    \label{SLC1}
    x \equiv 3\cdot17^{-1} ~\textrm{mod}~29
\end{equation}

So, we need to find the modular multiplicative inverse of $17$. 

<ol>

<li> <h3> <u> <a name="SLCUFLT"> Using Fermat's Little Theorem </a> </u> </h3> </li>

As, 29 is a prime, we can use FLT. Refer to <a href="/2020-05-19-fermats-little-theorem/#MMIULFT"> Modular Multiplicative Inverse using Fermat's Little Theorem </a>. We need to find,

\[ 17^{29 - 2} ~(\textrm{mod} ~ 29) \]
or,
\[ 17^{27} ~(\textrm{mod} ~ 29) \]

Refer to <a href="/2020-05-19-exponentiation-by-squaring/"> Exponentiation By Squaring </a> to compute the above term. After computing, we'll have,

\[ 17^{27} \equiv 12 ~(\textrm{mod}~29) \]

From \eqref{SLC1}, we then have,

\[ x \equiv 3\cdot17^{-1} ~(\textrm{mod}~29) \]
\[ x \equiv ((3 ~\textrm{mod}~29) \cdot (17^{-1} ~\textrm{mod}~29)) ~(\textrm{mod}~29)\]
\[ x \equiv 3 \cdot 12 ~(\textrm{mod}~29)\]
Finally, 
\[ x \equiv 7 ~(\textrm{mod}~29) \]


<li> <h3> <u> Using Euclidean Algorithm </u> </h3> </li>

We need to find $v$ such that,

\begin{equation}
    \label{SLCEA1}
    17v \equiv 1 ~(\textrm{mod}~29)
\end{equation}

\eqref{SLCEA1} can be rewritten as,

\[ 17v = 1 + 29w\]

For some $w \in \mathbb{Z}$. Rearranging the eqation we have,

\begin{equation}
    \label{SLCEA2}
    17v - 29w = 1 = \gcd(17,29)
\end{equation}

From <a href="/2020-05-19-bezouts-identity"> Bezout's Identity </a>, we know there exists solution to \eqref{SLCEA2}. After computing, we'll find that,

\[ 17 \cdot 12 + 29 \cdot (-7) = 1\]

Therefore, $v = 12$. And the rest follows similarly as <a href="#SLCUFLT"> Fermat's Little Theorem </a>.
