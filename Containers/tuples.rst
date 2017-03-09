Tuples
======

*Definition* - A tuple is an immutable list, i.e., it cannot be changed
once it is created.

.. code:: python

    a_tuple = (1, 2, 'this', 'that', False)
    b_tuple = tuple() # empty tuple
    c_tuple = tuple([1, 2, 3, 'this', 'that', False])

-  Tuples can be indexed and sliced, but must remain on the RHS of the
   assignment operator
-  being immutable, it only support ``count`` and ``index`` methods
-  as with any iterable ``in`` can also be used to find out if the tuple
   contains an item
-  a particular quirk of Python tuples is that when creating a tuple
   with a single value there has to be a comma after the first element
   like so: ``a_tuple = (1,)``
-  while tuples themselves are immutable, they can contain mutable items
   that can be modified

   .. code:: python

       t = tuple([1, 2, [3, 4], [5, 6]])
       print(t[-1])
       t[-1][0] = 'what'
       print(t[-1])

**What are they good for?**

-  faster than lists, since of a fixed length and are immutable
-  provide 'write-protected' data functionality
-  can be used as dictionary keys as they are immutable. Lists cannot

    In effect, tuple() freezes a list, and list() thaws a tuple.

    Note that multiple assignment is really just a combination of tuple
    packing and sequence unpacking.
