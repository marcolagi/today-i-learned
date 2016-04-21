# Regex and callbacks

When using `re.sub()`, it is possible to specify a callback that has access to
the groups of the regex pattern. `re.sub()` will then replace every occurrence
of the pattern with the result of that function.

For example:

    >>> import re
    >>> text = 'Today is 2016-4-21'
    >>> months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
    >>> callback = lambda x: '%s %s, %s' % (months[int(x.group(2))-1], x.group(3), x.group(1))
    >>> pattern = r'(\d+)-(\d+)-(\d+)'
    >>> re.sub(pattern, callback, text)
    'Today is Apr 21, 2016'
