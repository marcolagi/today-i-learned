# Decorators and memoization

Decorators can be used to memoize highly recorsive functions. Here is an
implementation that turns the expensive function calls of the Fibonacci sequence
into dictionary lookups:

    def memoize(f):
        cache = {}
        def decorated_function(*args):
            if args in cache:
                return cache[args]
            else:
                cache[args] = f(*args)
                return cache[args]
        return decorated_function

    @memoize
    def fib(n):
        return n if n < 2 else fib(n-2) + fib(n-1)

Aside, the default stack depth allowed by python is 1000, but it can be
increased with `sys.setrecursionlimit(value)`, where `value` is an integer.