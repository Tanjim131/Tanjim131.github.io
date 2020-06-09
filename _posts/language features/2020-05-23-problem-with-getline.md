---
layout: post
title: Be cautious when using std::getline!
subtitle: 
tags: [C++]
---

In ``C++``, you can take an input of whitespace separated string through ``std::getline``. But we should be careful when using it in conjunction with ``std::cin``.

``std::getline`` doesn't ignore leading whitespace character, but ``std::cin`` leaves the newline character (``\n``) in the ``iostream``. If ``std::getline`` is used after ``std::cin``, the ``std::getline`` sees this newline character as leading whitespace, thinks the input is finished and stops reading any further. 

The problem is demonstrated in the following example:

{% gist 4926d2e81050939e8a669454ba9ac1bd problem.cpp %}

The output:

{% gist 4926d2e81050939e8a669454ba9ac1bd output.txt %}

The ``name`` did not print because ``std::getline`` saw the newline character left from ``std::cin`` as leading whitespace. If you enter the name as ``ABC``, an implicit newline character will be appended at the end. So, the ``name`` variable becomes ``ABC\n``. ``std::getline`` sees this newline and stops reading!

## So what's the solution?

We can consume the trailing newline character left by ``std::cin`` before calling ``std::getline``. This can be done by using ``std::cin.ignore()`` to discard the rest of the input until we reach a fresh new line:

{% gist 4926d2e81050939e8a669454ba9ac1bd solution.cpp %}

You'll need to include ``<limits>`` to use ``std::numeric_limits``. 

``std::basic_istream<...>::ignore()`` is a function that discards a specified amount of characters until it either finds a delimiter or reaches the end of the stream.``ignore()`` also discards the delimiter if it finds it. The ``max()`` function returns the largest amount of characters that a stream can accept.

This is the signature of ``std::basic_istream<...>::ignore()``. You can call it with zero arguments to discard a single character from the stream, one argument to discard a certain amount of characters, or two arguments to discard count characters or until it reaches ``delim``, whichever one comes first. 

You normally use ``std::numeric_limits<std::streamsize>::max()`` as the value of count if you don't know how many characters there are before the delimiter, but you want to discard them anyway.

### Credit:
1. [This StackOverflow Answer](https://stackoverflow.com/a/21567292/7261925)
2. [MathBits](https://mathbits.com/MathBits/CompSci/APstrings/APgetline.htm)