---
layout: post
title: Reverse First K Elements of a Queue
tags: [Coding Interview]
---

Source: [GeeksForGeeks](https://practice.geeksforgeeks.org/problems/reverse-first-k-elements-of-queue/1)

We're given a queue $q$ and an integer $k$. We need to reverse the order of the $k$ elements of the queue, leaving the order of the remaining elements intact. 

We can solve this problem in two ways:

1.***Using an extra queue ($q^\prime$) and stack ($s$)***: Let the size of the queue $q$ be $n$. We'll push the first $k$ elements of the given queue $q$ to $s$. This way when we'll extract them from $s$, the order will be reversed. Now we'll push the remaining $n - k$ elements of $q$ to $q^\prime$. At this point, $q$ becomes empty. Now firstly we'll extract the elements from $s$ and push them in $q$. Finally, we'll extract the elements from $q^\prime$ and push them in $q$. 


{% gist 09b1d63ed76f92f3269370e33cd1faeb rfkeq_1.cpp %}


2.***Using recursion***: We can replace the explicit use of stack by implicitly using stack through recursion. Firstly we'll use recursion to reverse the order of the first $k$ elements of $q$ and add them at the end of $q$. Lastly, we'll extract the $n - k$ elements at the front of $q$ and push them at the end of $q$. 

{% gist 09b1d63ed76f92f3269370e33cd1faeb rfkeq_2.cpp %}


***Time and space complexity***: $\mathcal{O(n)}$ 