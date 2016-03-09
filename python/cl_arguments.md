# Command-line arguments

The standard library package `argparse` is useful to parse the list of
command line arguments of a python call (i.e. `sys.argv`). Another option is
the module `getopt`, but its API is a little less intuitive.

The `--help` option (which can also be shortened to `-h`) is already included
in the parser without explicitly declaring it. Same thing for error messages,
the parser handles them by default.

The parser is initialized with `ArgumentParser` and its main function is
`add_argument`.

Here is a complete example:

    import argparse

    parser = argparse.ArgumentParser(description='calculate X to the power of Y')

    # Positional argument
    parser.add_argument('base', type=int, help='the base')

    # Optional argument
    parser.add_argument('-e', '--exp', type=int, help='the exponent',
                        choices=[0, 1, 2], default=1, required=False)

    # Mutually-exclusive arguments
    group = parser.add_mutually_exclusive_group()
    group.add_argument('-v', '--verbose', action='store_true')
    group.add_argument('-q', '--quiet', action='store_true')

    args = parser.parse_args()
    answer = args.base**args.exp

    if args.quiet:
        print answer
    elif args.verbose:
        print '{} to the power {} is {}'.format(args.base, args.exp, answer)
    else:
        print '{}^{} == {}'.format(args.base, args.exp, answer)

Storing this in `args.py` and executing it will result in:

    $ python args.py -h
    usage: args.py [-h] [-e EXP] [-v | -q] base

    calculate X to the power of Y

    positional arguments:
      base               the base

    optional arguments:
      -h, --help         show this help message and exit
      -e EXP, --exp EXP  the exponent
      -v, --verbose
      -q, --quiet

    $ python args.py 4 -e 2 -vq
    usage: args.py [-h] [-e EXP] [-v | -q] base
    args.py: error: argument -q/--quiet: not allowed with argument -v/--verbose

    $ python args.py 4 -e 3 -v
    usage: args.py [-h] [-e {0,1,2}] [-v | -q] base
    args.py: error: argument -e/--exp: invalid choice: 3 (choose from 0, 1, 2)

    $ python args.py 4 --exp 2 -v
    4 to the power 2 is 16

A couple of comments:

- `argparse` treats all arguments as strings, unless otherwise specified with
`type`.
- `action='store_true'` simply stores `True` if the argument is present.
The default value is just `action='store'`, and other possible actions are
`action='count'` to count the number of times a flag is repeated (useful for
verbosity levels), `action='append'` to append all values of the argument in
a single list (useful to allow an option to be specified
multiple times) or even a custom function.
- `choices` adds constraints to the values an argument can take, `default`
specifies its value if absent, `required` can be `True` only for optional
arguments

