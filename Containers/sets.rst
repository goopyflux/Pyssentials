Sets in Python
==============

*Definition* - a set is an unordered colletction of unique values, with
a single set containing values of any immutable datatype.

-  Sets are created with the ``{}`` expression or with the ``set()``
   call
-  ``set()`` returns an empty set, while ``set(iterable)`` returns a set
   with only the unique items

.. code:: python

    a_set = {1, 2, 3}
    b_set = set() # empty set
    c_set = set([1, 2, 3, 4, 3, 2, 1]) # repeated values are dropped
    print(a_set)
    print(b_set)
    print(c_set)

*Trivia*: Due to older versions of Python 2, simply using ``{}`` to
create an empty set actually results in an empty ``dict``! Use ``set()``
instead.

Operations
----------

**Modifying a set**

-  possible with ``add`` and ``update`` methods.
-  ``add`` takes a single argument and adds the value to the set
-  ``update`` can take multiple arguments and adds them to the set
   repeatedly, i.e., a *union* of the set with itself and the arguments
-  ``discard`` - discards an element at a time and doesn't complain if
   the element is not fount
-  ``remove`` method removes an element at a time, but does raise a
   ``KeyError`` with element not fount
-  Like lists, ``pop`` and ``clear`` methods are also available to
   remove elements from a set

**Common Operations** - ``union``, ``intersection`` - ``difference`` -
to return the difference of two or more sets in a new set -
``symmetric_difference`` - to return all elements that are in exactly
one of the sets - ``symmetric_difference_update`` - updates a set with
the symmetric\_difference of itself and others - union, intersection and
symmetric\_difference are *symmetric* operations, i.e., the arguments
can be swapped and the results would be the same - ``issubset`` method
can be used to identify if another set is a subset of itself -
``issuperset`` method can be used to identify if this set contains
another set

**Usage**

-  eliminate duplicate entries/elements
-  create keys
-  test membership

Set Comprehension
-----------------

Similar to lists and dicts,
