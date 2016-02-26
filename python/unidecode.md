# Approximate Unicode with ASCII

The best python library for ASCII transliterations of Unicode text is
[Unidecode](https://pypi.python.org/pypi/Unidecode).

In first approximation, one could represent non-convertible Unicode characters
as ??? or with their codes (e.g. `é` becomes `U+00E9`), but that’s
useless to someone who actually wants to read what the text says. An actual
transliteration helps, for example, when building a URL out of
an article title, or when trying to match a Unicode string stored in a
database with one that was entered by a user with a US keyboard.

Unidecode uses hand-tuned character mappings between the two character sets
that try to imitate the mapping a human with a US keyboard would choose. It
converts fancy quotes to ASCII quotes, accented latin characters to unaccented,
and even attempts transliteration to deal with characters that don't have ASCII
equivalents. Since several Unicode strings can be transformed in the same ASCII
representation, this is a one-way transformation and some information is lost in
the process.

    >>> from unidecode import unidecode
    >>> unidecode(u'Mère Françoise called an Über')
    'Mere Francoise called an Uber'

