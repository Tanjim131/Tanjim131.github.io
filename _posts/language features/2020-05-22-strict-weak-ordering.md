---
layout: post
title: Strict Weak Ordering
subtitle: 
tags: [C++]
---

Allmost all C++ ``STL`` containers rely on strict weak ordering. For example, when sorting a ``std::vector`` using ``std::sort``, we have to either pass a comparator function or overload the $ < $ operator. For primitive data types like ``int`` or ``double``, we don't need to do this explicitly. But for user-defined data types, we have to do this explicitly. 

## What is a Strict Weak Ordering ?

A strict weak ordering is a binary predicate. 

A binary predicate is a binary function that takes two arguments as input and outputs ``true`` if a condition is met and ``false`` otherwise. For example, this binary function could be ``==`` operator. It will return ``true`` if the two arguments are equal. 

A strict weak ordering is a binary predicate that compares two objects, and returns ``true`` if the ``first`` argument precedes the ``second``. For examples, if you have a room full of person and you have to form a queue based
on their height, a person with "lesser" height will "precede" the person with greater height.

In the following criterion, we'll assume $f$ to be the binary predicate.

There's a definition that we need to be aware of. 

##### Definition of equivalence
Two objects $x$ and $y$ are equivalent if both $f(x, y)$ and $f(y, x)$ are $\textrm{false}$. Note that an object is always (by the irreflexivity invariant) equivalent to itself.

The standard mathematical definition of ***strict weak ordering*** requires four invariants to be met:
1. Irreflexivity - $f(x,x)$ must be $\textrm{false}$
2. Antisymmetry  - $f(x,y) = \textrm{true}$ implies $f(y,x) = \textrm{false}$
3. Transitivity  - If $f(x,y) = \textrm{true}$ and $f(y,z) = \textrm{true}$, then it implies $f(x,z) = \textrm{true}$.
4. Transitivity of equivalence - Equivalence (as defined above) is **transitive**: if $x \equiv y$ and $y\equiv z$, then $x \equiv z$. (This implies that equivalence does in fact satisfy the mathematical definition of an equivalence relation.) 

The first three axioms, irreflexivity, antisymmetry, and transitivity, are the definition of a ``partial ordering``; transitivity of equivalence is required by the definition of a ``strict weak ordering``.

One example can be given where the 3rd invariant is violated. For example in rock-paper-scissors, we have scissors $>$ paper, rock $>$ scissors, paper $>$ rock. In this case, it’s impossible to properly sort a ``vector`` of such elements, i.e. that it’s impossible to guarantee that for any member of the ``vector``, that element is always greater than (or equal to) any element to its left and smaller than (or equal) any element to its right.

    [rock, paper, scissors]
    // rock < paper
    // paper < scissors
    // but rock > scissors! 

## What can go wrong ?

If you don't correctly implement your comparator or don't overload $<$ correctly, your code could either crash or run into an infinite loop. Either way you are in unchartered waters. For example if you write the following:


{% highlight C++ linenos %}
bool operator < (int a, int b){                                             
    if(a < b) return false; 
}
{% endhighlight %}

Then, you're essentially saying to return true if $a >= b$. This breaks the irreflexivity invariant. For example, $ a \geq a $ should return ``false``, but in this case it's returning ``true``.

I've listed the possible scenarios below:

{% highlight C++ linenos %}
if(a < b) return true; // permitted                                       
if(b < a) return true; // permitted
if(a > b) return true; // permitted
if(b > a) return true; // permitted
if(a <= b) return true; // not permmited
if(b <= a) return true; // not permmited
if(a >= b) return true; // not permitted
if(b >= a) return true; // not permitted
if(a < b) return false; // not permitted
if(b < a) return false; // not permitted
if(a > b) return false; // not permitted
if(b > a) return false; // not permitted
if(a <= b) return false; // permitted
if(b <= a) return false; // permitted
if(a >= b) return false; // permitted
if(b >= a) return false; // permitted
{% endhighlight %}

## Correctly overloading $<$ operator

The only way to be perfectly sure that your comparator function is valid is to mathematically prove that it meets the requirement of strict weak ordering. One neat trick is using the ``std::tie`` method to create a ``std::tuple`` and then use it's $<$ operator which is known to behave correctly. Suppose the following ``class`` is defined:

{% highlight C++ linenos %}
class Person{                                                               
    int height;
    int age;
    std::string name;
};
{% endhighlight %}

Then the $<$ operator can be overloaded in the following manner:

{% highlight C++ linenos %}
class Person{                                                               
    int height;
    int age;
    std::string name;

    bool operator < (const Person &person) const{
        return tie(height, age, name) < tie(person.height, person.age, person.name);
    }
};
{% endhighlight %}

This will sort the persons first with height, then with age (tiebrekaer betwen persons with same height) and lastly with name (tiebreaker between persons with same height and age).

If you want a customer ordering, for example (age --> name --> height), then you could just change the ordering of the variables inside ``tie``:

{% highlight C++ linenos %}
class Person{                                                               
    int height;
    int age;
    std::string name;

    bool operator < (const Person &person) const{
        return tie(age, name, height) < tie(person.age, person.name, person.height);
    }
};
{% endhighlight %}



Source:
1. [Boost](https://www.boost.org/sgi/stl/StrictWeakOrdering.html#1)
2. [Codearchive](https://github.com/bashrc-real/Codearchive/blob/master/cpp/strict%20weak%20ordering.pdf)
3. [This medium Article](https://medium.com/@shiansu/strict-weak-ordering-and-the-c-stl-f7dcfa4d4e07)