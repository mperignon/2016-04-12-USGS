---
layout: page
title: Programming with Python
subtitle: Storing Multiple Values in Lists
minutes: 30
---
> ## Learning Objectives {.objectives}
>
> *   Explain what a for loop does.
> *   Correctly write for loops to repeat simple calculations.
> *   Trace changes to a loop variable as the loop runs.
> *   Trace changes to other variables as they are updated by a for loop.

In the first lesson we used NumPy arrays to manipulate temperature data. NumPy arrays are not built into Python: we had to import the library `numpy` in order to be able to use them. These data structures are the most useful for scientific computing because the allow us to easily do math on our data. For anyone who's programmed in Matlab or C before, these are also the most familiar data structure (which is why we introduce them first!).

One of the built-in data structures that you will definitely use extensively in Python is the list. Because they are built in, we don't need to load a library to use them. A list is exactly what it sounds like -- a sequence of things that don't all have to be the same type. Lists are ordered, so we can access the items through an integer index (like we did with NumPy arrays), and one list can simultaneously contain numbers, strings, other lists, numpy arrays, and even commands to run.

Lists are created by putting values, separated by commas, inside square brackets:

~~~ {.python}
odds = [1, 3, 5, 7]
print 'odds are:', odds
~~~
~~~ {.output}
odds are: [1, 3, 5, 7]
~~~

Because they are ordered, we can select individual elements from lists by indexing:

~~~ {.python}
print 'first and last:', odds[0], odds[-1]
~~~
~~~ {.output}
first and last: 1 7
~~~

> ## Negative indices?! {.callout}
> 
> One wonderful feature of sequences in Python is that they allow for indexing with respect to the end of the sequence by using negative values. An index of -1 refer to the last item in a list, -2 is the second to last, and so on. Try it out!
> 
> ~~~ {.python}
> text = "The quick brown fox jumped over the lazy dog."
> 
> print text[-1]
> print text[-4:-1]
> print text[-4:]
> print text[32:-1]
> ~~~
> ~~~ {.output}
> .
> dog
> dog.
> the lazy dog
> ~~~

We can change individual elements in a list by assigning new values to them:

~~~ {.python}
odds[-1] = 9
print 'odds are now:', odds
~~~
~~~ {.output}
odds are now: [1, 3, 5, 9]
~~~

There are many other ways to change the contents of lists besides assigning new values to individual elements:

~~~ {.python}
odds.append(11)
print 'odds after appending a value:', odds
~~~
~~~ {.output}
odds after appending a value: [1, 3, 5, 9, 11]
~~~

~~~ {.python}
del odds[0]
print 'odds after removing the first element:', odds
~~~
~~~ {.output}
odds after removing the first element: [3, 5, 9, 11]
~~~

~~~ {.python}
odds.reverse()
print 'odds after reversing:', odds
~~~
~~~ {.output}
odds after reversing: [11, 9, 5, 3]
~~~

There is one important difference between lists and strings: we can change the values in a list, but we cannot change the characters in a string.

~~~ {.python}
names = ['Newton', 'Darwing', 'Turing'] # typo in Darwin's name
print 'names is originally:', names
names[1] = 'Darwin' # correct the name
print 'final value of names:', names
~~~
~~~ {.output}
names is originally: ['Newton', 'Darwing', 'Turing']
final value of names: ['Newton', 'Darwin', 'Turing']
~~~

~~~ {.python}
name = 'Tell'
name[0] = 'B'
~~~
~~~ {.error}
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-15-220df48aeb2e> in <module>()
      1 name = 'Tell'
----> 2 name[0] = 'B'

TypeError: 'str' object does not support item assignment
~~~

> ## Ch-Ch-Ch-Changes {.callout}
> 
> Data which can be modified in place is called mutable, while data which cannot be modified is called immutable. Strings and numbers are immutable. This does not mean that variable names assigned to string or number objects are forever going to be assigned to those objects, but when we want to change the value of a string or number object, we can only replace the old value with a completely new value.
> 
> Lists and NumPy arrays, on the other hand, are mutable: we can modify them after they have been created. We can change individual elements, append new elements, or reorder the whole list. For some operations, like sorting, we can choose whether to use a function that modifies the data in place or a function that returns a modified copy and leaves the original unchanged.
> 
> Be careful when modifying data in place. If two variables refer to the same list and you modify a value in the list, it will change for both variables! If you want variables with mutable values to be independent, you must make a copy of the value when you assign it.
> 
> Because of pitfalls like this, code that modifies data in place can be more difficult to understand (and therefore to debug). However, it is often far more efficient to modify a large data structure in place than to create a modified copy for every small change. You should consider both of these aspects when writing your code.

If we make a list, (attempt to) copy it and then modify in place, we can cause all sorts of trouble:

~~~ {.python}
print 'Before:\n', 10 * '-'

odds = [1, 3, 5, 7]
primes = odds

print 'primes:', primes
print 'odds:', odds


print '\nAfter:\n', 10 * '-'

primes += [2]

print 'primes:', primes
print 'odds:', odds
~~~
~~~ {.output}

Before:
----------
primes: [1, 3, 5, 7]
odds: [1, 3, 5, 7]

After:
----------
primes: [1, 3, 5, 7, 2]
odds: [1, 3, 5, 7, 2]
~~~

The command `primes = odds` doesn't create a new copy of the list that the variable name `odds` is assigned to but instead assigns a second variable name to the same list. Essentially, the two variable names point to the exact same location in memory.

Since lists in Python can be modified in place (lists are mutable objects), changing the value of `primes` edits the contents of the part of memory that both `primes` and `odds` point to, causing the value of both variables to change.

To make a copy of a list that is independent of the original, we use the `list()` command:


~~~ {.python}
print 'Before:\n', 10 * '-'

odds = [1, 3, 5, 7]
primes = list(odds)

print 'primes:', primes
print 'odds:', odds


print '\nAfter:\n', 10 * '-'

primes += [2]

print 'primes:', primes
print 'odds:', odds
~~~
~~~ {.output}
Before:
----------
primes: [1, 3, 5, 7]
odds: [1, 3, 5, 7]

After:
----------
primes: [1, 3, 5, 7, 2]
odds: [1, 3, 5, 7]
~~~
