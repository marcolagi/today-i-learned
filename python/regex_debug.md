# Regex debugging

Debugging regular expressions can be a pain, and it's very easy to get them
wrong. The python regex parse tree can help with that. This can be printed
by passing the experimental `re.DEBUG` flag to `re.compile`.

For example, if you want to extract phone numbers with a pattern like
**(875) 333-4637**, but can't quite figure out what's wrong,

    >>> re.compile(r"(\d{3}) \d{3}-\d{4}", re.DEBUG)
    subpattern 1
      max_repeat 3 3
        in
          category category_digit
    literal 32
    max_repeat 3 3
      in
        category category_digit
    literal 45
    max_repeat 4 4
      in
        category category_digit

From which it's clear that the round brackets need to be escaped.

**NB**: `re` appears to cache patterns, because repeating the same `re.compile`
command returns the same object but doesn't print the parse tree. Type
`re.purge()` to purge this cache.

Another debugging method is to use online regex tools like
[Debuggex](https://www.debuggex.com/) or [Pythex](http://pythex.org/).




