---
layout: post
title: Count number of 1's in a bit string
tags: [C++]
---

Oftentimes when we're dealing with a number, we're interested in knowing the number of $1$'s in the binary representation of that number. It is also known as the [Hamming Weight](https://en.wikipedia.org/wiki/Hamming_weight). The ***Hamming weight*** of a string is the number of symbols that are different from the zero-symbol of the alphabet used. ***Hamming distance*** between two strings of equal length is the number of positions at which the corresponding symbols are different. This can be computer by $XOR$-ing the two strings. See the truth table for $XOR$ operation:

\\[
\begin{array}{|c|c|c|}
\\hline
  \text{A} & \text{B} & \text{A} \oplus \text{B} \\\ 
\\hline
   0 & 0 & 0 \\\
\\hline
   0 & 1 & 0 \\\
\\hline
   1 & 0 & 0 \\\ 
\\hline
   1 & 1 & 1 \\\
\\hline
\end{array}
\\]

So the output of $XOR$ operation is $1$ when the bits are different and $0$ otherwise. Let's look at an example. Say, $A = 1001011101$ and $B = 0111000100$ are two bit strings of length $10$. Following is the $XOR$ operation of them:

\begin{aligned}
\large{A} & = \Large{1001011101} \\\
\large{B} & = \Large{\underline{0111000100}}\\\
\large{A \oplus B} & = \Large{1110011001}
\end{aligned}

The output has $1$ in places where the bits of $A$ and $B$ differ, and $0$ otherwise, and so counting the number of $1$'s in $A \oplus B$ will give us the hamming distance between $A$ and $B$. 

Hamming weight is equivalent to the Hamming distance from the all-zero string of the same length. In case of our example above, if $B$ were $0000000000$ then the count of $1$'s in $A \oplus B$ would have given us the hamming weight of $A$. 

So in case of a binary string (containing only $0$'s and $1$'s), hamming weight is the number of $1$'s in the string.

There are a multitude of ways to count the number of $1$'s in a bit string. Let's go over them one by one.

### 1. Iterate all bits (Approach 1)
A number $n$ has exactly $\floor{log_2(n)} + 1$ digits in base $2$. So we can iterate over the bits/digits one by one and increment count if a bit is $1$:

{% gist f9fd35aef3216fb7e5c69f1bd702881e popcount1.cpp %}  

***Time Complexity***: $\mathcal{O}(\log_2(n))$. For all practical purposes it is $\mathcal{O}(1)$ because the largest representable integer $n$ is less than $2^{64}$ and so $\mathcal{O}(\log_2{64})$ $=$ $\mathcal{O}(64)$ $=$ $\mathcal{O}(1)$ (with a high constant).

### 2. Iterate all bits (Approach 2)
We can get rid of the ``floor`` and ``log`` function from the previous approach. We can get the least significant bit (LSB or rightmost bit) of a binary number by $AND$-ing it with $1$. After checking the LSB, we can right shift the number, (essentially halving it by $2$). After shifting the previous LSB will be gone the second rightmost bit will take its place. We'll continue right shifting and $AND$-ing until the number is greater than $0$.  

{% gist f9fd35aef3216fb7e5c69f1bd702881e popcount2.cpp %}

***Time Complexity***: Same as approach $1$.

### 3. Brian Kernighan's Algorithm

Subtracting $1$ from a decimal number flips/toggles all the bits to the right of of the rightmost set bit (or rightmost bit which has $1$), including itself.

For example, $(12)\_{10} = (00001100)\_{2}$. The rightmost set bit is at position $2$ from the right ($0$ based indexing). If we subtract $1$ from $12$, we get $(11)\_{10} = (00001011)\_{2}$. All the bits to the right of index $2$ including itself are flipped (meaning if it is $0$, it becomes $1$ and vice versa). 

Now what will happen if we perform an $AND$ operation between $12$ and $11$? $12~\&~11 = 00001000$. One important observation is that $AND$-ing $12$ and $11$ unset/cleared the rightmost set bit in $12$. So in general, if we perform an $AND$ operation between $n$ and $n - 1$ $ \left(n~\&~(n - 1)\right)$, then the rightmost set bit in $n$ will be unset or become $0$. 

Kernighan's algorithm perform this operation at each step until $n$ becomes $0$. Following is the implementation:

{% gist f9fd35aef3216fb7e5c69f1bd702881e popcount3.cpp %}

***Time Complexity***: As in each iteration the algorithm unset the rightmost set bit, the algorithm runs as many iterations as there are set bits. We know that a number $n$ has exactly $\floor{log_2(n)} + 1$ bits in base $2$. In the worst case, all the bits in $n$ are $1$ and so the running time becomes $\mathcal{O}(\log_2(n))$. The algorithm performs better when most bits in $x$ are $0$. 

Bonus: checking power of $2$ 

### 4. Using Built-in Functions of Compiler

Some compilers such as ``GCC`` support [intrinsics](https://stackoverflow.com/a/2268599/7261925). An intrinsic function is a function which the compiler implements directly when possible, rather than linking to a library-provided implementation of the function. Examples include ``strncpy`` and ``memset``.

For short strings, making a function call to ``strncpy``, which involves setting up a 'stack frame' with a return address, will consume more time than the actual copying of bytes does. Worse, the effect on [CPU pre-fetch buffers](https://en.wikipedia.org/wiki/Cache_prefetching) will stall the CPU execution for several clock cycles.

Instead, the intrinsic function is implemented by the compiler in lieu of a function call. In the example of ``strncpy``, the byte-copying code is emitted directly at the place where ``strncpy`` is invoked.

So in case of intrinsics in the best case, the compiler will emit a CPU instruction and in the worst case will generate a call to the library function. 

On the ``GCC`` compiler, you can just use:

```C++
int __builtin_popcount(unsigned int x)
int __builtin_popcountll(unsigned long long x)
```

``_builtin_popcount`` will use a processor instruction if available or an efficient library implementation otherwise. 

Intel Core processors introduced a [POPCNT](https://en.wikipedia.org/wiki/SSE4#POPCNT_and_LZCNT) instruction with the ``SSE4.2`` instruction set extension, first available in a Nehalem-based Core i7 processor, released in November 2008. AMD's Barcelona architecture introduced the advanced bit manipulation (ABM) ISA (Instruction Set Architecture) introducing ``POPCNT`` instruction as part of the ``SSE4a`` extensions in 2007. [Link to [Source](https://en.wikipedia.org/wiki/Hamming_weight#Processor_support)]

To utilize the ``POPCNT`` instruction, you should run the GCC compiler an option to enable the respective set of instructions that will tell the compiler that it can assume hardware support for ``POPCNT`` instruction. Following is the implementation:

{% gist f9fd35aef3216fb7e5c69f1bd702881e popcount4.cpp %}

You can also invoke ``POPCNT`` assembly instruction directly in the ``C++`` code:

{% gist f9fd35aef3216fb7e5c69f1bd702881e popcount5.cpp %}

***Time Complexity***: $\mathcal{O}(k)$ where $k = \floor{\log_2{n} + 1}$ is the number of bits in base $2$. For all practical purposes this is $\mathcal{O}(1)$ as we deal with fixed width integers (For example, $\mathcal{O}(32)$ $=$ $\mathcal{O}(1)$ for $32$ bit integers. 

### 5. Using C++ STL 

``C++`` offers the bit-array data structure ``std::bitset`` functionality to represent a number $n$ in its binary representation using fixed width. This probably is the most portable among the ones mentioned here and with ``GCC/CLANG`` with the right target options, you'll get hardware popcount support for architecture (for example ``x86-64``) that supports it.

{% gist f9fd35aef3216fb7e5c69f1bd702881e popcount6.cpp %}

``count`` method counts the number of bits that are set in $n$. After inlining ``bitset.count()`` compiles to a single ``__builtin_popcount`` call. [[Source](https://stackoverflow.com/questions/109023/how-to-count-the-number-of-set-bits-in-a-32-bit-integer#comment3829869_109069)]

***Time Complexity***: Theoretically, $\mathcal{O}(\ddfrac{\log_2(n)}{32})$ if bitset operates on $32$ bits at a time. The denominator can also be $64$ depending on the architecture. Practically $\mathcal{O}(1)$. Same as the previous approach. 

### 6. Using a lookup table

A pre-populated table lookup method can be very fast if your CPU has a large cache and/or you are doing lots of these instructions in a tight loop. However it can suffer because of the expense of a 'cache miss', where the CPU has to fetch some of the table from main memory. (Look up each byte separately to keep the table small.) [[Source](https://stackoverflow.com/a/109025/7261925)]

For a tradeoff between $2^{32}$ integer lookup table and iterating each bit individually, we can keep a lookup table which contains the number of set bits in the least significant $4$ bits. How many patterns are possible with $4$ bits? It's $2^4$ because we can place either $0$ or $1$ at any position and can reuse them for the remaining positions as well. 

Let's first see the implementation:

{% gist f9fd35aef3216fb7e5c69f1bd702881e popcount7.cpp %}

Now let's unroll this. What's the use of ``nibbleBits``? It's length is $16$, and is the same as the number of patterns representable with $4$ bits, starting with $0000$ and ending with $1111$. So ``nibbleBits[i]`` represents the number of set bits in the $i$-th ($ 0 \leq i < 16$) representation of $4$ bits starting from $0000$, or in other words the $i$-th lexicographically smallest pattern. For example, if $i = 7$, then the pattern is $0111$ and ``nibbleBits[7] = 3``.

So at each iteration we take the least significant $4$ bits of $n$, which is also called [nibble](https://en.wikipedia.org/wiki/Nibble), by $AND$-ing with $\text{0xf}$. In $32$ bit terms, $\text{0xf} = 0000\ldots(\text{28 0s})\ldots1111$, or the least significant $4$ bits are all $1$. So $AND$-with $\text{0xf}$ will give us the nibble of $n$ intact while the remaining bits of $n$ will become $0$. Then we do a $4$ bit shift to get the next nibble. We repeat this process until $n$ becomes $0$.

Notice that this implementation makes no assumption about native [word size](https://en.wikipedia.org/wiki/Word_(computer_architecture)) (typically word size is $4$ bytes or $8$ bytes). Word size refers to the number of bits processed by CPU at a time. The above process will also work in a machine where $1\text{byte} = 9\text{bits}$. [[Source](https://stackoverflow.com/a/113098/7261925)]

One important things to notice there is that the while loop will continue to run until there's a nibble to process. So technically the above process runs in $\mathcal{O}(\ddfrac{\floor{\log_2(n)}}{4})$ because there are $\floor{\log_2(n)} + 1$ number of bits and if we divide the number of bits by $4$, we'll get the number of nibbles. As the largest representable integer number is less than $2^{64}$, this approach is basically $\mathcal{O}(\ddfrac{64}{4}) = \mathcal{O}(16)$ or $\mathcal{O}(1)$. We can also let $n$ be as arbitrarily large as possible and do [Big-O analysis](https://en.wikipedia.org/wiki/Big_O_notation), but then the bitwise operation and the arithmetic operation won't remain constant. 

Also notice that there's nothing special about processing a nibble at each step. We could've processed more than $4$ bits at each iteration and it would have made the count of loop iteration much smaller. See [here](https://stackoverflow.com/a/109915/7261925) and [here](https://stackoverflow.com/a/131212/7261925) for a similar approach. But then we would have to store much more information in our lookup table. For example if we processed the last $8$ bits or a byte at a time, the complexity would've become $\mathcal{O}(\ddfrac{64}{8}) = \mathcal{O}(8)$ or $\mathcal{O}(1)$, but the size of the lookup table would've increased to $2^8 = 256$. In case of $2$ bytes or $16$ bits the lookup table's size becomes $2^{16} = 65536$. At $4$ bytes or $32$ bits the lookup table's size becomes $2^{32}$ and assuming $4$ bytes for each entry, it would require half a GB memory just to store the lookup table, which is just unrealistic. 

Notice that the lookup based approach is unbeatable is the table is in cache. But cache isn't very large and so you can't store large lookup tables in cache. Also if a cache miss takes $200$ cycles to fetch data from main memory and the CPU will stall. So there's a tradeoff. [[Source](https://stackoverflow.com/questions/109023/how-to-count-the-number-of-set-bits-in-a-32-bit-integer#comment32510_131212)]

There are other obscure approaches like [Bit Twiddling Hacks](https://graphics.stanford.edu/~seander/bithacks.html) explained [here](https://stackoverflow.com/a/29621923/7261925) and [here](https://stackoverflow.com/a/15979139/7261925) and [Hacker's Delight](https://books.google.com.bd/books?id=iBNKMspIlqEC&pg=PA66&redir_esc=y&hl=en#v=onepage&q&f=false). But I'll leave them aside and they require much more effort to understand and are not really readable at first glance.  