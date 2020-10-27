---
layout: post
title: Sum of All
tags: [Problem Solving]
---

Let's discuss a number theory problem from Brilliant. Problem link is given at the end.

We're asked to compute:

\\[ \sum_{x = 1}^{2015} \gcd(x, 2015)\\]

where $\gcd(a,b)$ stands for the greatest common divisor function.

We'll actually solve this problem without writing any computer program because where's the fun in that?

This problem is actually solvable in a variety of ways. I'll discuss one approach here, and I'll try to add different approaches some time in the future (no guarantees!)

The problem seems very difficult to solve by hand, but actually it's not. You need to the following to solve it:
- From $1$ to $n$, there are exactly $\floor{\ddfrac{n}{k}}$ numbers divisible by $k$

Let's first factorize $2015$. The prime factorization of $2015$ is:

\\[2015 = 5 * 13 * 31\\]

So the set of all divisors of $2015$ comprises $d = \\{5, 13, 65, 155, 403, 2015\\}$. We have excluded $1$ because all numbers excluding the numbers in $d$ have a $gcd$ of $1$ with $2015$.

Only the members of $d$ have a $\gcd > 1$ with $2015$. What are the possible $\gcd$s $ > 1 $? Let us list them:

\begin{eqnarray}
\gcd(5, 2015) & = & 5 \nonumber \newline
\gcd(13, 2015) & = & 13 \nonumber \newline
\gcd(31, 2015) & = & 31 \nonumber \newline
\gcd(65, 2015) & = & 65 & = & 5 * 13 \nonumber \newline
\gcd(155, 2015) & = & 155 & = & 5 * 31 \nonumber \newline
\gcd(403, 2015) & = & 403 & = & 13 * 31 \nonumber \newline
\gcd(2015, 2015) & = & 2015 & = &  5 * 13 * 31 \nonumber
\end{eqnarray}

So the possible $\gcd$ values are the same the member of $d$. Let's find out how many numbers are divisible by the numbers in $d$. One thing to note here is that, we want to find out how many numbers are divisible by ***only*** a particular member of $d$. For example, when figuring out how many numbers are divisible by $5$, we are interested in finding out numbers divisible ***only*** by $5$ and not any other number. As there could be numbers like $130$ which have both $5$ and $13$ or $465$ which have both $5$ and $31$ as factors, we have to exclude these numbers when calculating the numbers divisible by $5$. For this reason, it is helpful to start from the last member of $d$, find out its divisors, move to the member to its left until we've reached the first member, excluding extraneous number in the way (in each iteration the extraneous cases will only involve the cases processed previously).

How many number are from $1$ to $2015$ are divisible only by $2015$? The answer if $1$, $2015$ itself.  

How many number are from $1$ to $2015$ are divisible only by $403 = 13 * 31$? There are $\ddfrac{2015}{403} = 5$ numbers divisible by $403$ from $1$ to $2015$, but one of the numbers, namely $2015$ is divisible by $5$ also. So the actual answer is $ 5 - 1 = 4$.

How many number are from $1$ to $2015$ are divisible only by $155 = 5 * 31$? There are $\ddfrac{2015}{155} = 13$ numbers divisible by $155$ from $1$ to $2015$, but one of the numbers, namely $2015$ is divisible by $13$ also. So the actual answer is $ 13 - 1 = 12$.

Using similar reasoning, we find that there are $30$ numbers divisible only by $65 = 5 * 13$ from $1$ to $2015$.

Now we come to single digit numbers. How many numbers from $1$ to $2015$ are divisible only by $5$? The answer is $\floor{\ddfrac{2015}{5}} - 1 - 12 - 30 = 360$ (subtracting the numbers that has divisors either $13$ or $31$ or both). Similarly $120$ numbers are divisible only by $13$ and $48$ numbers divisible only by $31$. 

Now that we've all the counts, let's express them in concrete terms. Let, $A$, $B$ and $C$ be the set of numbers divisible by $5$, $13$ and $31$ respectively. Using [Inclusion-Exclusion Principle](https://en.wikipedia.org/wiki/Inclusion%E2%80%93exclusion_principle) we find that,

\begin{aligned}
|A \cup B \cup C| = |A| + |B| + |C| - |A \cap B| - |A \cap C| - |B \cap C| + |A \cap B \cap C|
\end{aligned}

So from $1$ to $2015$ there are $403 + 155 + 65 - 31 - 13 - 5 + 1 = 575 $ numbers divisible by either $5$, $13$ or $31$. So there are $2015 - 575 = 1440 $ numbers not divisible by any of $5$, $13$ or $31$. 

Finally we can now plug in the numbers to find the answer,

\begin{aligned}
\sum_{x = 1}^{2015} \gcd(x, 2015)    & = \gcd(5,2015) * 360 + \gcd(13,2015) * 120 + \gcd(31,2015) * 48 \newline
                                        & \quad + \gcd(65, 2015) * 30 + \gcd(155,2015) * 12 + \gcd(403,2015) * 4 \newline
                                        & \quad + \gcd(2015, 2015) * 1 + \sum_{x \not\in \\{5,13,31,65,155,403,2015\\}}\gcd(x,2015) * 1440 \newline
                                    & = 5 * 360 + 13 * 120 + 31 * 48 + 65 * 30 + 155 * 12 + 403 * 4 \newline
                                        & \quad + 2015 * 1 + 1 * 1440 \newline
                                    & = 13725
\end{aligned}

We can verify our answer by writing a simple ``C++`` program:

{% gist 7f5689ecde2af6e111ef66e98f17a712 %}

***Problem link*** :- [Sum of all](https://brilliant.org/problems/sum-of/)