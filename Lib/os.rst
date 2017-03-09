The Python ``os`` Module
========================

From the docstring for ``os.py``

    Programs that import and use 'os' stand a better chance of being
    portable between different platforms. Of course, they must then only
    use functions that are defined by all platforms (e.g., unlink and
    opendir), and leave all pathname manipulation to os.path (e.g.,
    split and join).

Current working directory
-------------------------

.. code:: python

    import os

    print(os.getcwd()) # current working directory
    print(os.chdir('/usr/local/bin')) # change the current working directory
    print(os.getcwd())

``os.chdir`` returns a ``FileNotFoundError`` if the path is not found

Directories and Filenames
-------------------------

The module ``os.path`` has functions for manipulating filenames and
directory names.

Joining strings to form paths
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: python

    import os

    print(os.path.join('/usr/local/', 'bin/file'))
    print(os.path.join('/usr/local', 'bin/file')) # missing '/' is automatically appended
    print(os.path.sep) # stores the OS depndent path separator(?)

Splitting pathnames
~~~~~~~~~~~~~~~~~~~

.. code:: python

    import os

    pathname = '/usr/local/lib'
    os.path.split(pathname) # returns a tuple(head, tail) where tail is everything after the last os.path.sep in pathname

    os.path.splitext(pathname) # splits into extension and everything else; could be '' if no '.' is found in pathname

.. code:: python

    import os

    print(os.path.expanduser('~'))
    print(os.path.expandvars('$PATH'))

File Metadata
~~~~~~~~~~~~~

Use ``os.stat`` to access metadata about the file like date created,
date modified, size, etc.

*Tip*: The file time stamps are not in a human readable format. Use the
``time`` module to format it into readable calendar date and time
format.

Constructing Paths
~~~~~~~~~~~~~~~~~~

To get the full path for files, say in the current working directory or
on a list of files without the path, the ``os.path.abspath`` (for
absolute path) and the os.path.realpath\` (for canonical path) can be
useful

**Difference** - ``realpath`` parses symbolic links to get the real path
to the file being linked whereas ``abspath`` just stops at the link and
doesn't follow it.

.. code:: python

    import os

    print(os.path.abspath('/usr/local/python3'))
    print(os.path.realpath('/usr/local/python3'))
