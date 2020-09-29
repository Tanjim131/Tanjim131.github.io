---
layout: post
title: Implement Queue Using Linked List
tags: [Coding Interview]
---

Source: [GeeksForGeeks](https://practice.geeksforgeeks.org/problems/implement-queue-using-linked-list/1)

We have to implement a queue using a linked list. We're given two pointers ``front`` and ``rear`` of the linked list.

Our strategy is to append new elements at the end of linked list (``push`` operation) and delete elements from the start of the linked list (``pop`` operation). 

For ``pop`` operation, if ``front`` is a null pointer, then we'll return ``-1`` as the linked list (or queue) is empty.

Initially, ``front`` and ``rear`` both pointers are empty. So if a enqueue operation occurs, then we'll initialize both the ``front`` and ``rear`` pointer. Then it'll look something like the following:

<figure>
<img src="/assets/img/coding interview/queue using linked list.svg" width="800" height="500" class="center">
<figcaption> Front and Rear initialized for the first time </figcaption>  
</figure>

For subsequent push/enqueue operations, we just need to update the ``rear`` pointer. The situation will look something like this after a few push/enqueue operation:

<figure>
<img src="/assets/img/coding interview/queue using linked list 2.svg" width="800" height="500" class="center">
<figcaption> Scenario after a few push/enqueue operation </figcaption>  
</figure>

Now if a pop/dequeue operation occurs, we need to advance the ``front`` pointer. There is a special case here. If after several updates, the ``front`` pointer becomes null, then it means that the queue or linked list has become empty. If that happens, then we need to set the ``rear`` pointer to null as well.

Here's the final implementation:

{% gist d3982f5a0c308c54261eb6cf6d97a027 %}

Time and Space Complexity: $\mathcal{O(1)}$