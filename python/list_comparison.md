# Comparison of unordered lists

When two lists of arbitrary objects should be considered equal regardless of
their order, there are a couple of ways to compare them, according to the
nature of their elements.

If the elements are **hashable**, the `Counter()` method is best:

    from collections import Counter

    def are_lists_equal(list1, list2):
        return Counter(list1) == Counter(list2)

If the elements are **orderable**, the `sorted()` method is best:

    def are_lists_equal(list1, list2):
        return sorted(list1) == sorted(list2)

If the objects are not hashable and not sortable, one has to use equality:

    def are_lists_equal(list1, list2):
        return len(list1)==len(list2) and all(list1.count(i)==list2.count(i) for i in list1)
