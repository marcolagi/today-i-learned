# Class equality

When writing custom classes, it's often important to allow equivalence by means
of the `==` and `!= `operators. In Python, this is made possible by implementing
the `__eq__` and `__ne__` special methods, respectively.

Since it's a generic feature of classes, a useful strategy pattern is to break
equivalence out into a class, and inherit it in classes where you want that
functionality.

    class Equality(object):

        def __eq__(self, other):
            return (isinstance(other, self.__class__)
                    and self.__dict__ == other.__dict__)

        def __ne__(self, other):
            return not self.__eq__(other)

    class Foo(Equality):

        def __init__(self, item):
            self.item = item

When `__eq__` and `__ne__` are defined in this way, the following is possible:

    >>> a = Foo(1)
    >>> b = Foo(1)
    >>> a is b
    False
    >>> a == b
    True

Otherwise, `a == b` will evaluate to `False` because it really
runs `a is b`, a test of identity.


