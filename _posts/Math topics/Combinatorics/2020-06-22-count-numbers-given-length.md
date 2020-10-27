---
layout: post
title: How many numbers of some given length are there?
tags: [Combinatorics]
---

You are given a length $i$. You are asked to compute how many valid numbers of length $i$ are there. For example, if $i = 2$, then the valid numbers of length $2$ ranges from $10$ to $99$. So in total there are $99 - 10 + 1 = 90$ valid numbers of length $2$. I am using the word ***valid*** to disregard numbers with leading zeroes (for example $01$ or $003$).

What is smallest number of length $i$? The most significant digit (or leftmost digit) in the smallest number of length $i$ is $1$ and the rest of the $i - 1$ digits are all $0$. So the smallest number is a power of $10$. We know that $10^{k}~(k \geq 0) $ has exactly $k$ zeroes and comprises length $k + 1$ (the $+1$ indicates the leading $1$). For example, $10^0 = 1$ has $0$ zeroes and length $1$. $10^1 = 10$ has $1$ zero and length $2$ and so on. So, smallest number of length $i$ has $i - 1$ zeroes and it can be expressed as $10^{i - 1}$. 

What is the largest number of length $i$? All of $i$ digits are $9$ in the largest number. This number is just $1$ short of the next power of $10$. For example, when $i = 2$, the largest $2$ digit number is $99$ which is just $1$ short of $100$. The next power of $10$ (after the largest number of length $i$) has $i$ zeroes and comprises $i + 1$ digits and can be expressed as $10^{i}$. As the largest number of length $i$ is just $1$ short of this power $10$, the largest number of length $i$ can be expressed as $10^i - 1$. 

Now that we've established the smallest and the largest number of length $i$, we can now compute the range. 

\begin{eqnarray}
\textrm{range(i)} & = & \textrm{largest number} - \textrm{smallest number} + 1 \nonumber \newline
& = & (10^i - 1) - (10^{i - 1}) + 1 \nonumber \newline
& = & 10^i - 10^{i - 1} \nonumber \newline
& = & 10^{i - 1}(10 - 1) \nonumber \newline
& = & 9 \times 10^{i - 1}
\end{eqnarray}

So there are a total of $9 \times 10^{i - 1}$ numbers of length $i$. 