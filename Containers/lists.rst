Lists in Python
===============

Defined using ``[]`` (ex. ``a_list = []``).

Basic operations
----------------

**Element access** - indexing (zero, positive and negative indices),
slicing

**List modification**

-  add items with ``+`` (not recommended for large lists, as it creates
   copies of the lists), ``append()`` method, ``extend()`` method,
   ``insert(index, value)``\ method
-  remove items with ``pop()``, which can also accept an index location,
   ``remove``, which requires the value (instead of index) to remove the
   value or ``clear`` to clear the entire list

*``append`` vs ``extend``* - append takes just one argument of any type
and adds it to the list. len(list after append) = len(list before
append) + 1 - extend takesa single argument, which is always a list and
adds each item in the list as an item. len(list after extend) = len(list
before extend) + len(items being added)

**Searching and Sorting** - ``index`` method returns the index where
item was found - ``count`` method returns the total number of
occurrences of an item - ``reverse`` method reverses a list, while
``sort`` method sorts a list **in place** (make a copy first, if this is
not preferable, see tip below). ``sort`` also takes the optional
``key=None`` and ``reverse=False`` arguments.

*Tip*: Interestingly, simply assigning a list to another variable seems
to create a reference to the same object in memory. It doesn't guarantee
a copy operation in the pure sense and is not safe from modifications to
the original list. Use the ``copy`` method instead to create a copy that
persists even after the original list has been modified.

A list is considered ``True`` anytime it contains an item (or is
non-empty). For instance, ``['False']`` is a ``True`` list (confusing,
but true)

Notice that methods like insert, remove or sort that only modify the
list have no return value printed – they return the default None. This
is a design principle for all mutable data structures in Python

Lists can be used as stacks as they support LIFO operations easily with
``append`` and ``pop`` methods Lists are inefficient as queues (FIFO
operation). Use ``collections.deque`` instead

List Comprehensions
-------------------

Comprehension provides a way to map a list into another list, by either
applying a mapping function or modifying each element of the list.

.. code:: python

    a_list = [1, 2, 3, 4, 5]
    a2_list = [a**2 for a in a_list]

*Under the hood* - Python takes each element of ``a_list`` in the
variable ``a``, applies the *function* ``a**2`` (squaring the value) and
saves the squared value to a new list in memory. After processing all
the elements from ``a_list``, it assigns the list in memory to
``a2_list``

**List comprehension the functional programming way**

.. code:: python

    a2_list = list(map(lambda x: x**2, xrange(1,6)))
    print(a2_list)

List comprehensions for filtering items
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Additionally, list comprehensions can include an ``if`` expression that
will be called for each element of the list and will be included in the
final list only if the condition is satisfied (or not, depending on how
the ``if`` expression is structured)

.. code:: python

    import os
    import glob

    pyfiles = [f for f in glob.glob('/usr/local/bin/py*') if f.find('python') > 0] # list only files containing 'python' in their name

    There is no limit to how complex a list comprehension can be

**Flattening a list of lists**

.. code:: python

    vec = [[1,2,3], [3,4,5], [5,6,7]]
    flat_vec = [num for v in vec for num in v]

**Complex expressions and nested functions for list comprehensions**

.. code:: python

    from math import pi
    pi_precision = [str(round(pi, i)) for i in range(1,11)]

Nested List Comprehensions
--------------------------

The initial expression in a list comprehension can be any arbitrary
expression, including another list comprehension

.. code:: python

    matrix = [
        [1, 2, 3, 4],
        [5, 6, 7, 8],
        [9, 10, 11, 12],
    ]

    matrixT = [[row[i] for row in matrix] for i in range(3)] # transpose operation

    coolT = list(zip(*matrix)) # WOW! returns tuples of unpacked matrix list

Looping Techniques
------------------

In addition to list comprehensions,

-  use ``in`` to simply get each item from a sequence
-  use ``enumerate`` to get the index and item from a sequence
-  use ``zip`` to loop over two or more sequences at the same time
-  use ``reversed()`` function to loop over a sequence backwards
-  use ``sorted()`` to loop over the sorted sequence
-  use ``sorted(reverse=True)`` to loop over the reverse-sorted sequence
-  use ``sorted(key=len, reverse=True)`` to loop over the sequence in
   the decreasing order of length
