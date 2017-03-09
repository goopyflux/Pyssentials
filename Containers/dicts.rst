Dictionaries in Python
======================

*Definition* - an unordered set of ``key-value`` pairs that are
optimized to retrieve the value, using a key (not the other way around)

-  can be created with the ``{}`` or ``dict()`` call
-  keys to a dict are case sensitive

Dictionary Comprehension
========================

Similar to list comprehension, but constructs a ``dict`` instead, with a
couple of differences:

-  use ``{}`` instead of ``[]``
-  since dicts need key-value pairs to be generated, there needs to be
   two expressions separated by a ``:`` (as opposed to a single
   expression for list)

Assuming immutable values, dict comprehension can be used to swap
existing ``key:value`` into a new ``value:key`` dict

.. code:: python

    a_dict = {'a':1, 'b':2, 'c':3}
    print(a_dict)
    b_dict = {value:key for key, value in a_dict.items()}
    print(b_dict)

*Tip*: always use ``items`` method to loop over key-value pairs of the
dict. It is faster and better
