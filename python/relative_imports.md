# Relative imports

`pylint`, a popular Python style-checker, complains when modules in the
same package are imported without specifying the full package path.

    W0403: Relative import %r, should be %r
    Used when an import relative to the package directory is detected.

This warning is raised, for example, if packages are structured like this:

    /nolan
      /__init__.py
      /inception.py
      /interstellar.py
    /aronofsky

and in the `interstellar` package one writes `import inception`.

The problem of `import inception` is that python doesn't know whether its an
absolute import or a relative import. `inception` could be a module in python's
path, or a package in the current module. This is quite annoying when a local
package has the same name as a python standard library package.

Python 3 has disabled implicit relative imports altogether; imports are now
always interpreted as absolute, meaning that in the above example
`import inception` will always import the top-level module.

The solution is to always write relative imports explicitly:

    from . import inception



