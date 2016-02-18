# Decorators and docstrings

A **decorator** is a callable that takes a function as an argument and returns
another function, usually a modified version of the original function with added
functionality. Here is an example of defining a decorator called `verbose`
and applying it to `sqrt`:

    def verbose(original_function):

        def new_function(*args, **kwargs):
            name = original_function.__name__
            print 'Entering "%s"' % name
            original_function(*args, **kwargs)
            print 'Exiting "%s"' % name

        return new_function

    @verbose
    def sqrt(num):
        '''Calculate the square root of a number'''
        print num**0.5

The line that starts with `@` is the **decoration line** (**nb**: not a
decorator, the decorator is just the function). Equivalent to the last 4 lines
is the following:

    def sqrt(num):
        '''Calculate the square root of a number'''
        print num**0.5
    sqrt = verbose(sqrt)

Here's what happens by calling `sqrt`:

    >>> sqrt(4)
    Entering "sqrt"
    2.0
    Exiting "sqrt"

But calling `help` on `sqrt` produces:

    >>> help(sqrt)
    Help on function new_function in module __main__:

    new_function(*args, **kwargs)
    (END)

The docstring is lost because the decorated function `new_function` did not
inherit it. Not only that, the function name has changed! The solution is to
copy over these two attributes while defining the new function:

    def verbose(original_function):

        def new_function(*args, **kwargs):
            name = original_function.__name__
            print 'Entering "%s"' % name
            original_function(*args, **kwargs)
            print 'Exiting "%s"' % name

        new_function.__name__ = original_function.__name__
        new_function.__doc__ = original_function.__doc__

        return new_function

    @verbose
    def sqrt(num):
        '''Calculate the square root of a number'''
        print num**0.5

Now we have:

    >>> help(sqrt)
    Help on function sqrt in module __main__:

    sqrt(*args, **kwargs)
        Calculate the square root of a number
    (END)

