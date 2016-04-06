# Partial string format

Positional formatting in Python can be done with the following syntax:

    >>> "%s is more than %d feet tall."  % ('Shaq', 7)
    "Shaq is more than 7 feet tall."

This includes options for padding strings, aligning them, truncating etc. But
if not all arguments are given,

    >>> "%s is more than %d feet tall."  % ('Shaq')
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    TypeError: not enough arguments for format string

Here is a trick to get around it by using **named placeholders**,

    >>> "%(name)s is more than %%(height)d feet tall."  % {'name': 'Shaq'}
    "Shaq is more than %(height)d feet tall."
    >>> "Shaq is more than %(height)d feet tall." % {'height': 7}
    "Shaq is more than 7 feet tall."