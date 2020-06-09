---
layout: post
title: Using std namespace before C functions in C++
subtitle: Should you include std namespace before using C functions? If so, why? 
tags: [C++]
---

There are tons of ``C`` functions available in ``C++``. There's one that known to all. Yes, I'm talking about ``printf``. But there's a difference between header in ``C`` and in ``C++``. ``C++`` uses the same header names from ``C``, but the ``.h`` extensions are removed and ``c`` prefix is added in all cases. Also whenever you use a function from the standard library, you have to include ``std::`` namespace. 

Now given that, ``printf`` is declared in ``cstdio``, the ``C++`` version of ``stdio.h``, should you use ``printf`` like this:

{% gist b742cad28edcccd166fa93845fde6053 test-1.cpp %}

Or like this:

{% gist b742cad28edcccd166fa93845fde6053 test-2.cpp %}


The answer is you can choose either one. Check out this answer:

<figure>
<img src="/assets/img/language_features/using-std-before-c-functions-pic1.png" width="700" height="300" class="center">
</figure>

And this comment:

<figure>
<img src="/assets/img/language_features/using-std-before-c-functions-pic2.png" width="700" height="100" class="center">
</figure>

There can be some conflicts for example in case of ``abs`` function. So you're better of using ``std::`` prefixes.  

Check out [this stackoverflow answer](https://stackoverflow.com/questions/32606023/when-using-c-headers-in-c-should-we-use-functions-from-std-or-the-global-na) which discusses the topic in great detail.