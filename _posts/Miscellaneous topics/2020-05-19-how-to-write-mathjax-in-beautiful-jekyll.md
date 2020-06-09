---
layout: post
title: A guide to writing latex in github pages
subtitle: 
tags: [Miscellaneous, LaTeX]
comments: true
---

In this post, I'll write about how I integrated latex typesetting into beautiful-jekyll based web page. Check out [beautiful-jekyll website](https://github.com/daattali/beautiful-jekyll) to learn more about how to set up a personal website/blog within minutes. 

I used mathjax version 3.0 for writing latex. One of the nice things about beautiful-jekyll is that a lot of options are supported out of the box. So, it's just a matter off specifying some options instead of writing them yourself.

<!-- $\colorbox{MistyRose}{_config.yml}$ -->

To start, we'll look at the `_config.yml`  file. YAML files contains fields as ``name:value`` pair.
Scroll down to the end until you find ``markdown`` field. It should be set to `kramdown`. A few lines below that you should find:

{% gist 1fbd8d5629e2d62135340f5ae85d4585 latex.yml %}

The ``input`` field should be set to ``GFM``. You just have to add ``math_engine: mathjax``. 

That's all there is to tweak in the ``_config`` file.

Now browse to ``/_includes/head.html``. At the bottom of the page, before the ``</head>`` tag, add the following lines:

{% gist 1fbd8d5629e2d62135340f5ae85d4585 latex.js %}

You'll find the detailed explanation of the various fields and their uses on [MathJax 3.0 Documentation](http://docs.mathjax.org/en/latest/). I won't bother you with the details here. 

That's all you need to do. You can now start writing latex. 

One thing to look out for is to be careful about writing latex in markdown files. MathJax doesn't support ``\emph``, ``\begin{enumerate} ... \end{enumerate}`` or other text-mode macros or environments. You have to use ``HTML`` or ``markdown`` to handle such formatting tasks. 

Also check out [this awesome stackexchange post](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference) for a comprehensive reference to writing MathJax!

If you have any questions, feel free to contact me! 
