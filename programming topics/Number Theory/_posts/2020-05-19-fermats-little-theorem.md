---
layout: post
title: Fermat's Little Theorem
subtitle: I have a truly marvelous subtitle for this post which this margin is too narrow to contain. 
tags: [Number Theory]
comments: true
---


<b> Statement </b>: 

\\[ a^{m} \equiv a ~(\textrm{mod}~m)\\]

Where, $m$ is a prime. In other words, $a^{m} - a$ is a multiple of $m$. If $ m \nmid a$, then we have,

\begin{equation}
    \label{FLT1}
    a^{m - 1} \equiv 1 ~(\textrm{mod}~m)
\end{equation}

<h2> <u> <a name="MMIUFLT"> Modular Multiplicative Inverse using FLT </a> </u> </h2>

When we have, $m \nmid a$, \eqref{FLT1} can be rewritten,

\\[ a \cdot a^{m -2} \equiv 1 ~(\textrm{mod}~m) \\]

Therefore, $a^{m-2} ~(\textrm{mod}~m)$ is the modular multiplicative inverse of $a~(\textrm{mod}~m)$. We can calculate $a^{m - 2}~(\textrm{mod}~m)$ by <a href="/2020-05-19-exponentiation-by-squaring"> Exponentiation By Squaring </a>. 
