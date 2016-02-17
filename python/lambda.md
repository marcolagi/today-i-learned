# Scope of lambda functions

Here's a behavior that baffled me:

    >>> def print_str(text): print text
    >>> lambdas = [lambda: print_str(i) for i in ['a', 'b', 'c']]
    >>> lambdas[0](); lambdas[1](); lambdas[2]()
    c
    c
    c

The problem turns out to be the following. When a lambda function is created,
it doesn't make a copy of the variables in the scope that it uses. It maintains
a reference to the environment so that it can look up the value of the variable
later. In the example above, at the end of the loop, the variable `i` has
value `c`. So when the function is called later, it will look up the value of
`i` in the environment that created it, i.e. `c`. In fact,

    >>> i = 'd'
    >>> lambdas[0](); lambdas[1](); lambdas[2]()
    d
    d
    d

A solution to this problem is to capture the value of `i` at the time that the
lambda is created by using it as the default value of an optional parameter:

    >>> lambdas = [lambda i=i: print_str(i) for i in ['a', 'b', 'c']]
    >>> lambdas[0](); lambdas[1](); lambdas[2]()
    a
    b
    c







