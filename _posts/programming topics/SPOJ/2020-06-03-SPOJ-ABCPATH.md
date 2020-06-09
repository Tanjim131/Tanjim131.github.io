---
layout: post
title: SPOJ - ABCPATH
tags: [SPOJ]
---

This is a simple $2d$ Graph Traversal Problem. We can use multi-source ***BFS*** or ***DFS***. 

We check each cell of the $2d$ grid and if it contains $A$ then we launch a DFS from that cell. In each DFS call, we check the neighboring $8$ cells (as diagonal cells are considered neighboring cells also), and if it contains the next lexicographical character, we move on to that cell. In each valid iteration, we increment the current path length by $1$, and we update the max path length also. 

Here's the implementation in ``C++``:

{% gist edff0409aebc8776540854281238ea4c %}