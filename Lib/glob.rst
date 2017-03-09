Python ``glob`` Module
======================

From the docstring for ``glob``

    Filename globbing utility.

**What is globbing?**

From google instant search result -

    Globbing is the process of expanding a non-specific file name
    containing a wildcard character into a set of specific file names
    that exist in storage on a computer, server, or network. A wildcard
    is a symbol that can stand for one or more characters

In Python 3.6, ``glob`` internally uses ``iglob`` which is the iterator
version of ``glob`` and is more efficient with memory and faster.

The module relies on the ``os``, ``re`` and the ``fnmatch`` modules to
carry out its functionality.
