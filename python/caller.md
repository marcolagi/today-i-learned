# Where am I calling that function?

For profiling and debugging, it's useful to know when and where in your code
you're calling a given low-level function. Here is a decorator that can be
applied to any function to achieve just that:

    import sys

    def log_caller(original_function):

        def new_function(*args, **kwargs):
            called = original_function.__name__
            caller = sys._getframe().f_back.f_code.co_name
            print 'Calling "%s" from "%s"' % (called, caller)
            original_function(*args, **kwargs)

        return new_function

    @log_caller
    def my_func1():
        return

    def my_func2():
        my_func1()

This will print:

    >>> my_func2()
    Calling "my_func1" from "my_func2"

The function `sys._getframe()` returns a frame object from the call stack. If
the optional integer `depth` is not given, it returns the frame at the top of
the call stack. `f_back` moves down in the stack one level, so that
`sys._getframe().f_back` is equivalent to `sys._getframe(1)`.

There are other ways to do that, for example using the `inspect` module.

