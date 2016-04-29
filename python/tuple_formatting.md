# Tuple formatting

The `%` operator in python takes a tuple to format a string:

    >>> 'To print: %s' % 'A' == 'To print: %s' % ('A',)
    True

So while the left-hand side works with a list or a dictionary, it doesn't work
with a tuple:

    >>> 'To print: %s' % ['A', 'B']
    "To print: ['A', 'B']"

    >>> 'To print: %s' % ('A', 'B')
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    TypeError: not all arguments converted during string formatting

The operator expects only one argument to be converted, and it gets two. A
simple solution is to wrap the tuple in another one-element tuple,

    >>> 'To print: %s' % (('A', 'B'), )
    "To print: ('A', 'B')"

or to use the `.format()` method.




