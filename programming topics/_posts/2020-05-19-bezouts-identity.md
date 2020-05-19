---
layout: post
title: Bezout's Identity
subtitle: Statement and Demonstration of Bezout's Identity
tags: [Number Theory, Problem Solving]
comments: true
---

<b>  Statement </b>: $\forall a,b \in \mathbb{Z}, \exists x,t \in \mathbb{Z}$, such that $ ax + by = \gcd (a,b) $.

<b> Demonstration </b>: Let $a = 432$ and $b = 126$. Then from <a href = "/2020-05-18-why-euclidean-algo-works"> Euclid's algorithm </a>, it follows that, 


\begin{equation}
    \label{bz:gcd1}
    432 = 3\cdot126 + 54 
\end{equation}

\begin{equation}
    \label{bz:gcd2}
    126 = 2\cdot54  + 18
\end{equation}

\begin{equation}
    \label{bz:gcd3}
    54  = 3\cdot18  +  0
\end{equation}


As, $\gcd(18,0) = 18$, therefore, $\gcd(432,126) = 18$. Now we want to figure out $x$ and $y$ $\in \mathbb{Z}$ such that,

\\[ 432\cdot x + 126\cdot y = \gcd(432,126) = 18 \\]

We start from \eqref{bz:gcd1}, and rewrite it as,

\begin{equation}
    \label{bz:gcd4}
    54 = 432 - 3\cdot126
\end{equation}

We also rewrite, \eqref{bz:gcd2} as,

\begin{equation}
    \label{bz:gcd5}
    18 = 126 - 2\cdot54
\end{equation}

Now we replace, \eqref{bz:gcd4} in \eqref{bz:gcd5},

\\[ 18 = 126 - 2\cdot(432 - 3\cdot126) \\]
\\[ = 126 - 2\cdot432 + 6\cdot126 \\]
\\[ = -2\cdot432 + 7\cdot126 \\]

Therefore, $x = -2$ and $ y = 7$.

<b> Observation </b>: $x$ and $y$ are co-prime and $x \mid a$ and $y \mid b$.

<b> <i> Question </i> </b>: Is this the only solution $?$

<b> <i> Answer </i> </b>: No. We can actually find the system of equations for which the identity holds.

The technique is to find an equal quantity that we can add with $432$ and subtract from $126$ or vice versa. What that means is, we'll rewrite the equation as, 

\begin{equation}
    \label{bz:allsol1}
    432\cdot(-2 + p) + 126\cdot(7 + q) = 18
\end{equation}

Where, $432\cdot p$ and $126\cdot q$ will cancel each other out (Opposite signs).

How can we can get an equal quantity my multiplying both $432\cdot p$ and $126\cdot q~?$ We have to choose $p$ and $q$ as such that after multiplying with $432$ and $126$ respectively, it will give $\rm{lcm}(432,126)$. Now, $\rm{lcm}(432,126) = 3024$. So,

\\[ 432\cdot p = 3024 \\]
\\[ p = 7 \\]

And, as $p$ and $q$ has to be opposite, we get,

\\[ 126\cdot q = -3024 \\]
\\[ q = -24 \\]

So, $(p,q) = (7,-24)$. $(p,q) = (-7,24)$ will also work. <br> <br> For $(p,q) = (7,-24)$, \eqref{bz:allsol1} becomes,

\begin{equation}
    \label{bz:allsol2}
    432\cdot(-2 + 7) + 126\cdot(7 - 24) = 18
\end{equation}

For any multiples of $\rm{lcm}(432,126)$, \eqref{bz:allsol2} becomes,

\begin{equation}
    432\cdot(-2 + 7m) + 126\cdot(7 - 24m) = 18
\end{equation}

So, the values of $x$ and $y$ for which the identity holds true, are the solutions to the following system of equations,

\\[ x = -2 + 7m \\]
\\[ y = 7 - 24m \\]

Where, $m \in \mathbb{Z}$.

<h2> <u> Corollary of Bezout's Lemma </u> </h2>

<b> <i> Question </i> </b>: If $n \mid ab$ and $n \nmid a$, does that imply $n \mid b ~?$ 

<b> <i> Answer </i> </b>: No.

<b> <i>  <u> Claim </u> </i> </b>: If $n \mid ab$ and $\gcd(n,a) = 1$, then $n \mid b$.

<b> <i> <u> Proof </u> </i> </b>: Since, $\gcd(n,a) = 1$, $\exists x,y \in \mathbb{Z} $ such that $ nx + ay = 1$. Multiplying both sides by $b$,

\begin{equation}
\label{eqn:gcd1}
bnx + bay = b 
\end{equation}

Now, as $n \mid ab$, we have $ nk = ab $, for some $k \in \mathbb{Z}$. Replacing that in \eqref{eqn:gcd1},

\begin{equation}
\label{eqn:gcd2}
bnx + nkb = b 
\end{equation}

The left hand side of the equation \eqref{eqn:gcd2} is divisible by $n$. As both sides of the equation must hold, we conclude that, $n \mid b$. &nbsp; $ \blacksquare $