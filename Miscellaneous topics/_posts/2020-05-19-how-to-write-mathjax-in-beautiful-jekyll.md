---
layout: post
title: A guide to writing latex in github pages
subtitle: 
tags: [Miscellaneous, LaTeX]
comments: true
---

In this post, I'll write about how I integrated latex typesetting into beuatiful-jekyll based web page. Check out <a href="https://github.com/daattali/beautiful-jekyll"> beautiful-jekyll website </a> to learn more about how to set up a personal website/blog within minutes. 

I used mathjax version 3.0 for writing latex. One of the nice things about beautiful-jekyll is that a lot of options are supported out of the box. So, it's just a matter off specifying some options instead of writing them yourself.

To start, we'll look at the  $\colorbox{MistyRose}{_config.yml}$ file. YAML files contains fields as **``name:value``** pair.
Scroll down to the end until you find **``markdown``** field. It should be set to **``kramdown``**. A few lines below that you should find:

{% highlight yaml linenos %}
kramdown:
  input: GFM
  math_engine: mathjax # you can also set this field to 'katex'
{% endhighlight %}

The **``input``** field should be set to **``GFM``**. You just have to add **``math_engine: mathjax``**. 

That's all there is to tweak in the **``_config``** file.

Now browse to **``/_includes/head.html``**. At the bottom of the page, before the **``</head>``** tag, add the following lines:

{% highlight javascript linenos %}
<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script>
MathJax = {
    loader: {load: ['[tex]/newcommand', '[tex]/color']},
    tex: {
        packages: {'[+]': ['newcommand', 'color']},
        inlineMath: [['$','$'], ['\\(', '\\)']],
        displayMath: [['$$', '$$'],['\\[', '\\]']],
        macros: {
            bold: ['{\\bf #1}',1],
            ddfrac: ['{\\frac{\\displaystyle #1}{\\displaystyle #2}}', 2],
            abs: ['\\left\\lvert #2 \\right\\rvert_{\\text{#1}}', 2, ""],
            floor: ['\\left\\lfloor #2 \\right\\rfloor_{\\text{#1}}', 2, ""],
            sfrac: ['{ \\frac {\\ #1 \\ }{#2}}', 2],
            lcm: ['\\operatorname{lcm}#1', 1]
        },
        processEscapes: true,
        processEnvironments: true,
        processRefs: true,
        digits: /^(?:[0-9]+(?:\{,\}[0-9]{3})*(?:\.[0-9]*)?|\.[0-9]+)/,
        tags:  'ams',
        tagSide: 'right',
        tagIndent: '0.8em', 
        useLabelIds: true,  
        multlineWidth: '85%',
    },
    chtml: {
        scale: 1.2
    },
    svg: {
        scale: 1.3
    }
};
</script>
<script id="MathJax-script" async
    src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js">
</script>
{% endhighlight %}

You'll find the detailed explanation of the various fields and their uses on <a href="http://docs.mathjax.org/en/latest/"> MathJax 3.0 Documentation </a>. I won't bother you with the details here. 

That's all you need to do. You can now start writing latex. 

One thing to look out for is to be careful about writing latex in markdown files. MathJax doesn't support **``\emph``**, **``\begin{enumerate} ... \end{enumerate}``** or other text-mode macros or environments. You have to use **``HTML``** to handle such formatting tasks. 

If you have any questions, feel free to contact me! 
