---
layout: post
title: Maximum Value of nCr
tags: [Combinatorics]
---

The number of ways we can choose $H$ objects from $N$ objects where the order doesn't matter is expressed by $\displaystyle{N \choose H}$ where $N,H$ are integers and $N > 0$, $0 \leq H \leq N$. We're interested in finding the maximum value of $\displaystyle{N \choose H}$.

Recall that,

\begin{eqnarray}
\label{binomial1}
{N \choose H} = {N \choose N - H}
\end{eqnarray}

We'll first prove that the values of $f(H) = \displaystyle{N \choose H}$ are symmetric with respect to $\floor{\ddfrac{N}{2}}$ and $\ceil{\ddfrac{N}{2}}$ for a fixed value of $N$. (This is also visible from [Pascal's Triangle](https://en.wikipedia.org/wiki/Pascal%27s_triangle)).

If $N$ is even, then we have only one value (namely, $\ddfrac{N}{2}$) with respect to which $f(H)$ is symmetric. If $H = \ddfrac{N}{2}$, then $N - H = \ddfrac{N}{2}$. Here, $f\left(\floor{\ddfrac{N}{2}}\right) = f\left(\ceil{\ddfrac{N}{2}}\right) = f(\ddfrac{N}{2})$

But if $N$ is odd, then there's two values (namely,$\ddfrac{N - 1}{2} = \floor{\ddfrac{N}{2}}$ and $\ddfrac{N + 1}{2} = \ceil{\ddfrac{N}{2}}$) with respect to which $f(H)$ is symmetric. If $H = \floor{\ddfrac{N}{2}}$, then $N - H = \ceil{\ddfrac{N}{2}}$ and vice-versa. Here, $f\left(\floor{\ddfrac{N}{2}}\right) = f\left(\ceil{\ddfrac{N}{2}}\right)$

Let, $M = \ddfrac{N}{2}$. We let $H = M - K$ such that $0 \leq K \leq M$. When $K = 0$, $H = M$ and when $k = M$, $H = 0$. So the values of $H$ are decreasing in the range $\left[0, M\right]$. Now $N - H$ $=$ $N - (M - K)$ $=$ $N - M + K$. Now there are three cases:

1. $N$ is even and $M = \ddfrac{N}{2}$. Then,
    - $N - M = N - \ddfrac{N}{2}$ $ = N - \ddfrac{N}{2}$ $ = \ddfrac{N}{2}$ $= M$ 
2. $N$ is odd and $M = \floor{\ddfrac{N}{2}}$. Then,
    - $N - M = N - \floor{\ddfrac{N}{2}}$ $ = \floor{N - \ddfrac{N}{2}}$ $ = \ceil{\ddfrac{N}{2}}$
3. $N$ is odd and $M = \ceil{\ddfrac{N}{2}}$. Then,
    - $N - M = N - \ceil{\ddfrac{N}{2}}$ $ = \ceil{N - \ddfrac{N}{2}}$ $ = \floor{\ddfrac{N}{2}}$

From \eqref{binomial1}, we have $f(H) = f(N - H)$. For case $(1)$, 

\begin{eqnarray}
f(H) & = & f(N - H) \nonumber \\\
\implies f(M - K) & = & f(N - M + K) \nonumber \\\
\label{binomial2}
\implies f(M - K) & = & f(M + K)
\end{eqnarray}

\eqref{binomial2} is symmetric with respect to axis $x = M$. 

For case $(2)$,

\begin{eqnarray}
f(H) & = & f(N - H) \nonumber \\\
\implies f(M - K) & = & f(N - M + K) \nonumber \\\
\label{binomial3}
\implies f(\floor{\ddfrac{N}{2}} - K) & = & f(\ceil{\ddfrac{N}{2}} + K)
\end{eqnarray}

From \eqref{binomial3}, when $K = 0$, we have $f(\floor{\ddfrac{N}{2}}) = f(\ceil{\ddfrac{N}{2}})$ and when $ K = M$ we have, $f(\floor{\ddfrac{N}{2}} - \floor{\ddfrac{N}{2}}) = f(\ceil{\ddfrac{N}{2}} + \floor{\ddfrac{N}{2}})$ or $f(0) = f(N)$.

For case $(3)$,

\begin{eqnarray}
f(H) & = & f(N - H) \nonumber \\\
\implies f(M - K) & = & f(N - M + K) \nonumber \\\
\label{binomial4}
\implies  f(\ceil{\ddfrac{N}{2}} - K) & = & f(\floor{\ddfrac{N}{2}} + K)
\end{eqnarray}

From \eqref{binomial4}, when $K = 0$, we have $f(\ceil{\ddfrac{N}{2}}) = f(\floor{\ddfrac{N}{2}})$ and when $ K = M$ we have, $f(\ceil{\ddfrac{N}{2}} - \ceil{\ddfrac{N}{2}}) = f(\floor{\ddfrac{N}{2}} + \ceil{\ddfrac{N}{2}})$ or $f(0) = f(N)$.

Case $(2)$ and $(3)$ are basically same. As $\ceil{\ddfrac{N}{2}} = \floor{\ddfrac{N}{2}} + 1$, we could've replaced this identity in \eqref{binomial3} and derived at \eqref{binomial4},

\begin{eqnarray}
f(\ceil{\ddfrac{N}{2}} - K - 1) & = & f(\floor{\ddfrac{N}{2}} + K + 1) \nonumber \\\
\implies f(\ceil{\ddfrac{N}{2}} - (K + 1)) & = & f(\floor{\ddfrac{N}{2}} + (K + 1)) \\\
\end{eqnarray}

So in cases $(2)$ and $(3)$, where $N$ is odd, we have $f(H)$ is symmetric with respect to $\floor{\ddfrac{N}{2}}$ and $\ceil{\ddfrac{N}{2}}$. 

Now that we've shown $f(H)$ to be symmetric, we'll prove that $f(H)$ increases monotonically (non-decreasing) in the range $0 \leq H \leq \floor{\ddfrac{N}{2}}$ or $0 \leq H \leq \ceil{\ddfrac{N}{2}}$. To prove this, we take to consecutive terms $f(H^\prime)$ and $f(H^\prime + 1)$ and observe that in order to make $f(H)$ monotonically increasing, we must have,

\begin{eqnarray}
f(H^\prime + 1) & \geq & f(H^\prime) \nonumber \\\
\implies {N \choose H^\prime + 1} & \geq & {N \choose H^\prime} \nonumber \\\
\implies \ddfrac{N \choose H^\prime + 1}{N \choose H^\prime} & \geq & 1 \nonumber \\\
\implies \ddfrac{\cancel{N!}~H^\prime!~(N - H^\prime)!}{(H^\prime + 1)!~(N - H^\prime - 1)!~\cancel{N!}} & \geq & 1 \nonumber \\\
\implies \ddfrac{\cancel{H^\prime!}~(N - H^\prime)~\cancel{(N - H^\prime - 1)!}}{(H^\prime + 1)~\cancel{H^\prime!}\cancel{(N - H^\prime - 1)!}} & \geq & 1 \nonumber \\\
\implies \ddfrac{N - H^\prime}{H^\prime + 1} & \geq & 1 \nonumber \\\
\implies H^\prime & \leq & \ddfrac{N - 1}{2} \nonumber \\\
\implies H^\prime & \leq & \floor{\ddfrac{N}{2}}
\end{eqnarray}

Using $f(H^\prime)$ and $f(H^\prime - 1)$ we can follow a similar reasoning to derive at $H^\prime \leq \ceil{\ddfrac{N}{2}}$. 

As we've proved $f(H)$ is increasing up to $\floor{\ddfrac{N}{2}}$ or $\ceil{\ddfrac{N}{2}}$ and the values of $f(H)$ are symmetric, so we can conclude that the function is decreasing beyond $\ceil{\ddfrac{N}{2}}$. It can also be seen by calculating the inequality $f(H^\prime + 1) \leq f(H^\prime)$ or $f(H^\prime) \leq f(H^\prime - 1)$. 

So the maximum value of $f(H)$ occurs at $\floor{\ddfrac{N}{2}}$ or $\ceil{\ddfrac{N}{2}}$. 

### Useful links:
- [Binomial Coefficient Properties](https://en.wikipedia.org/wiki/Binomial_coefficient#Binomial_coefficients_as_polynomials)
- [This Stackexchange Question](https://math.stackexchange.com/questions/823693/prove-that-binom-nk-frac-n-n-kk-viewed-as-a-function-of-k)
- [Another Stackexchange Question](https://math.stackexchange.com/questions/722952/how-do-you-prove-n-choose-k-is-maximum-when-k-is-lceil-tfrac-n2-rcei)
- [Yet Another Stackexchange Question](https://math.stackexchange.com/questions/3717719/find-the-condition-where-the-product-of-two-factorials-is-minimized)
