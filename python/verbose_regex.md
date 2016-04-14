# Verbose regex

Regular expressions can get very messy very fast. They are a compact notation,
but they’re not terribly readable. To alleviate this, there is a
compilation flag in the `re` module that allows for inline documentation, i.e.
to write regexes that look nicer and are more readable, allowing to visually
separate logical sections of the pattern and add comments (with `#`,
whitespaces and carriage returns are ignored). For example, one can turn this

    pat = re.compile(r"\s*(?P<header>[^:]+)\s*:(?P<value>.*?)\s*$")

into this

    pat = re.compile(r'''
        \s*                   # Skip leading whitespace
        (?P<header>[^:]+)     # Header name
        \s* :                 # Whitespace, and a colon
        (?P<value>.*?)        # The header's value
        \s*$                  # Trailing whitespace to end-of-line
    ''', re.VERBOSE)







