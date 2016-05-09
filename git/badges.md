# Badges on GitHub

Badges (or shields) are a great way to inform the audience about the version, license,
test coverage, number of downloads, project management, funding, code quality,
dependency and build status
of a GitHub project. They are tipically added to the README.rst file of the
project like so:

    .. image:: https://coveralls.io/repos/github/[USER_NAME]/[REPO_NAME]/badge.svg
        :target: https://coveralls.io/github/[USER_NAME]/[REPO_NAME]
        :alt: Coverage Status

where `image` specifies the URI to be displayed, `target` makes the image into
a hyperlink reference (i.e. clickable) and `alt` is the alternate text,
displayed by applications that cannot display images, or spoken by applications
for visually impaired users. Equivalently, for a README.md:

    [![Coverage Status](https://coveralls.io/repos/github/[USER_NAME]/[REPO_NAME]/badge.svg)](https://coveralls.io/github/[USER_NAME]/[REPO_NAME])

where `[REPO_NAME]` is the name of the GitHub project and `[USER_NAME]` the name of
the Github username. This particular badge
displays the test coverage of your project. Here is a partial list of the most
useful badges that could be included (tailored to python projects):

#### Version

    .. image:: https://img.shields.io/pypi/v/[REPO_NAME].svg
        :target: https://pypi.python.org/pypi/[REPO_NAME]
        :alt: Latest Version

#### License

    .. image:: https://img.shields.io/pypi/l/[REPO_NAME].svg
        :target: https://pypi.python.org/pypi/[REPO_NAME]
        :alt: License

#### Python compatibility

    .. image:: https://img.shields.io/pypi/pyversions/[REPO_NAME].svg
        :target: https://pypi.python.org/pypi/[REPO_NAME]
        :alt: Python Versions

#### Test installation and build

    .. image:: https://travis-ci.org/[USER_NAME]/[REPO_NAME].svg?branch=master
        :target: https://travis-ci.org/[USER_NAME]/[REPO_NAME]
        :alt: CI

#### Test coverage

    .. image:: https://coveralls.io/repos/github/[USER_NAME]/[REPO_NAME]/badge.svg?branch=master
        :target: https://coveralls.io/github/[USER_NAME]/[REPO_NAME]?branch=master
        :alt: Coverage

#### Code quality

    .. image:: https://landscape.io/github/[USER_NAME]/[REPO_NAME]/master/landscape.png
       :target: https://landscape.io/github/[USER_NAME]/[REPO_NAME]/master
       :alt: Health

#### Tasks and project management

    .. image:: https://badge.waffle.io/[USER_NAME]/[REPO_NAME].png?label=ready&title=Ready
       :target: https://waffle.io/[USER_NAME]/[REPO_NAME]
       :alt: Tasks

These services often use webhooks, which allow the badge to be updated at every
`git push` once you've oauth'ed your GitHub account.
