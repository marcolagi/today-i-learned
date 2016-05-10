# Submit a package to PyPI

**PyPI**, the Python Package Index, is a repository of software for the Python
programming language. Assuming the package to submit is `mypackage` and that
its code is hosted on GitHub, these are the steps to follow.

1. create an account on [PyPI Test](https://testpypi.python.org/pypi?%3Aaction=register_form)
and one on [PyPI Live](https://pypi.python.org/pypi?%3Aaction=register_form).

1. create a `.pypirc` configuration file and put it in your home folder:

        [distutils]
        index-servers =
          pypi
          pypitest
        [pypi]
        repository=https://pypi.python.org/pypi
        username=your_username
        password=your_password
        [pypitest]
        repository=https://testpypi.python.org/pypi
        username=your_username
        password=your_password

1. make sure your project has a `setup.py` file in the root directory, containing
metadata about `mypackage`. At the bare minimum,

        from distutils.core import setup
        setup(
          name = 'mypackage',
          packages = ['mypackage'],
          version = '0.1',
          description = 'A random test lib',
          author = 'My name',
          author_email = 'myemail@example.com',
          url = 'https://github.com/myname/mypackage',
          download_url = 'https://github.com/myname/mypackage/tarball/0.1',
          keywords = ['testing', 'logging', 'example'],
          classifiers = [],
        )

    The `download_url` is a link to a hosted file with your repository's code.
    Github will host this for you, but only if you create a `git tag`:

        git tag 0.1 -m "Adds a tag so that we can put this on PyPI.".
        git push --tags origin master

    Github will create tarballs for download at
    https://github.com/{username}/{module_name}/tarball/{tag}.

1. make sure your project has a `LICENSE.txt` file and a `README.[rst|md]` file.
reStructuredText (.rst) is recommended.

1. upload `mypackage` to PyPI test:

        python setup.py register -r pypitest
        python setup.py sdist upload -r pypitest

1. if you don't get any errors, upload `mypackage` to PyPI live:

        python setup.py register -r pypi
        python setup.py sdist upload -r pypi





