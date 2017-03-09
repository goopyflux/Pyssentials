Notes from the **Python Cookbook**

Chapter 1 Data structures and algorithms
========================================

Unpacking a known fixed-length sequence into separate variables
---------------------------------------------------------------

Any sequence (or iterable) can be unpacked into variables by the
assignment operator. The only requirement is that the number of
variables being assigned to (the left hand side of the assignment
operator) be equal to the length of the sequence.

.. code:: python

    p = (4, 5)
    x, y = p

The beauty of Python is that it allows us to unpack any object that
happens to be iterable (ex. files, strings, iterators, generators,
etc.), not just the standard objects like lists, tuples, etc.

How about files?

.. code:: python

    with open('test.txt', 'w') as f:
        fwrite('line one\nline two\nline three\n')

    with open('test.txt') as f:
        a, b, c = f

    print(a, b, c)

*Key*: Number of variables should match the number of items contained in
the iterable object, else it returns a ``ValueError``

*Tip*: Use the ``_`` variable to discard certain values. It can be used
multiple times in the same assignment statement

Unpacking elements from a sequence of arbitrary unknown length
--------------------------------------------------------------

While the above examples are all fixed length sequences, for iterable
sequences with unknown (or arbitrary) length, the Python "star
expressions" can be used to address the problem of "too many values to
unpack" error.

.. code:: python

    with open('test.txt') as f:
        a, *b = f

    print(a)
    print(b)

The star expression can occur anywhere in the assignment but can occur
only once in the statement (unlike the ``_`` variable which can occur
multiple times).

The star expression is very handy when processing records and
selectively extracting data from certain fields, while ignoring the
others or processing strings with certain delimiters from which certain
sub-fields need to be extracted

.. code:: python

    line = 'hello:this:string:234:is:342:seperated:5442:by:/usr/local/bin'
    *_, folder = line.split(':')
    print(folder)

*Tip*: combine ``*_`` to bulk discard values after unpacking

The starred variable will always be a list, this seems intentional as it
would lead to more unpacking subsequently (see trivia below).

*Trivia*: ``*`` is also used to unpack iterable sequence into positional
arguments to a function

Notice the difference in the output of the following two calls:

.. code:: python

    # continued from previous example
    print(b)
    print(*b) # Python unpacks b into positional arguments beore the print() call

The start expression essentially lets one split a sequence into 'one vs
the rest'. This approach can be used recursively to act on each item of
the sequence in a recursive fashion. However, this is not recommended,
since recursion is not a particularly strong feature of Python.

Keeping the last N items
------------------------

**Problem** Keeping a limited *history* of the last few items of a
sequence.

**Solution** The ``collections.deque`` is perfect for keeping the N
elements. It implements FIFO operation (which lists are not optimized to
do).

.. code:: python

    from collections import deque
    n = 5
    q = deque(maxlen=n)
    q.append(1)

In general, use FIFO structures for instances where the old items need
to be removed from one end and new items need to be added to the other.

*Brief look at generators* - generators are essentially iterable
functions.

.. code:: python

    def count_down(n):
        while n > 0:
            yield n
        n -= 1

    for i in count_down(10):
        print(i)

    c = count_down(5)
    next(c) # prints 5
    next(c) # prints 4 etc.

Refer to the example code for usage of generators and deque.

*Note*: Adding or popping items from either end of a queue has O(1)
complexity. This is unlike a list where inserting or removing items from
the front of the list is O(N).

Finding the N largest or smallest items from a collections...
-------------------------------------------------------------

*...when N is sufficiently small compared to the size of the collection*

Use ``heapq`` module's ``nlargest`` or ``nsmallest`` (depending on the
situation) to get the desired result.

Interestingly in the help for heapq.nlargest or heapq.nsmallest, it
mentions that the usage is similar to using ``sorted()`` in combination
with the ``reverse`` keyword (if largest) and with slicing operator
``[:]`` to get the n elements

.. code:: python

    import heapq

    nums = [234, 64, 2, 3, 85, -1345, -84, -1, 4363, 33, 21, 624, 8]
    n = 5

    nlarge = heapq.nlargest(n, nums)
    print(nlarge)
    print(sorted(nums, reverse=True)[:n])

    nsmall = heapq.nsmallest(n, nums)
    print(nsmall)
    print(sorted(nums)[:n])

-  Seems to be that for N ~ size of the sequence, ``sorted`` might be
   better.
-  if N = 1, just use ``min`` and ``max``. It is better and faster
-  use heapq when there are a lot of items in the sequence and N is
   relatively smaller compared to the size

Implementing a Priority Queue with ``heapq``
--------------------------------------------

Need to revisit this section later

Mapping keys in a dictionary to multiple values
-----------------------------------------------

To build a *multidict* (one that holds multiple values for each key or a
sequence for each key), use the ``defaultdict`` from the ``collections``
module.

.. code:: python

    from collections import defaultdict

    d = defaultdict(list) # a dict based on lists

    d['a'].append(1) # using the list append method
    d['a'].append(2)
    d['a'].append(3)

    d = defaultdict(set) # a dict based on sets

    d['a'].add(1) # using the set add method
    d['a'].add(2)
    d['a'].add(3)

*Note* ``defaultdict`` will automatically add key entries for all keys
accessed, even if the key is not present in the dict. If this is
undesirable, the workaround is to use the ``setdefault()`` method on a
regular dictionary.

.. code:: python

    # continued from above
    print(d)
    print(d['b'])
    print(d)

``defaultdict`` simplifies the problem of initializing a multidict to
null values or zeros.

Keeping dictionary in order
---------------------------

Typically a dictionary key:value pair is not stored in the same order it
was entered if using the default dictionary constructs ``{}`` or
``dict``. If order is important, then use the ``OrderedDict`` from the
``collections`` module.

*Use case*: when building a mapping that might be serialized later
(think JSON). However, it doesn't come without an overhead.
``OrderedDict`` maintains a doubly linked list internally and is hence
more memory intensive and less efficient compared to a regular dict.
Hence not recommended for large data.


