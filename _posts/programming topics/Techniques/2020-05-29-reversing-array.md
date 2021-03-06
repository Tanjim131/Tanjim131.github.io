---
layout: post
title: How to reverse an array
tags: [C++]
---

You can reverse an array both iteratively and recursively in $\mathcal{O}(n)$ time with $\mathcal{O}(1)$ space.

Here's the ``iterative`` version:

{% gist 5cdb60a62706816e760a7838bb9126d9 iterative.cpp %}

***Output***:

{: .box-warning}
Before reversing: $\textrm{50 11 25 37 43}$

{: .box-error}
After reversing: $\textrm{43 37 25 11 50}$

The iterative version repeatedly swaps the $i$-th element with the $(\textrm{size} - 1 - i)$-th element. Given $\textrm{size} = 5$ in the above code, it swaps the $1st$ element with the $5th$ element and the $2nd$ element with the $3rd$ element. After that it stops. We only need to check up to the first $\floor{\ddfrac{size}{2}}$ elements.

Here's the ``recursive`` version:

{% gist 5cdb60a62706816e760a7838bb9126d9 recursive.cpp %}

***Output***:

{: .box-warning}
Before reversing: $\textrm{50 11 25 37 43}$  

{: .box-error}
After reversing: $\textrm{43 37 25 11 50}$

The recurisve version works by repeatedly narrowing the array. At first the array size is $5$ in the above example. Then we swap the first and last element. After that we recursively do this for the middle $\textrm{arrSize} - 2$ sized array. In each recursive step, we only swap the first and last element of the array. In the above example, after the first swap is executed, the array becomes $[11, 25, 37]$ for the next recurisve call by calling $\textrm{reverseArray(arr + 1, arrSize - 2)}$. $\textrm{arr}$ points to the first location in the contiguous memory allocated for this array. $\textrm{arr + 1}$ just advanced this location by $1$. We're decreasing by $2$ because in each step we operate on two elements, $\textrm{arr}[0]$ and $\textrm{arr}[\textrm{arrSize} - 1]$. 

You can also reverse the array with $\mathcal{O}(n)$ space by using an extra array.

If you're using ``std::vector`` container in ``C++``, then there's this ``STL`` function called ``std::reverse`` that can reverse the ``std::vector``.