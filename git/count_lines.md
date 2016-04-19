# Count lines of code of a GitHub repo

The "Language statistics" section on Github displays the percentage of the a
repository that is written in a language. It doesn't, however, display how many
lines of code the project consists of. This would be useful to get an impression of
the scale and complexity of a project: 500 lines of code implies a relatively
simple project, 100,000 lines of code implies a complex one.

To achieve this:

1. Install [CLOC](https://github.com/AlDanial/cloc) (Count lines of code) with
your package manager (e.g. `brew install cloc`)

1. Save the following code in a file, say `cloc-git`:

        #!/usr/bin/env bash
        git clone --depth 1 "$1" temp-linecount-repo &&
        printf "('temp-linecount-repo' will be deleted automatically)\n\n\n" &&
        cloc temp-linecount-repo &&
        rm -rf temp-linecount-repo

1. run `chmod +x cloc-git`

1. move the file to a folder in your `PATH`, like `/usr/local/bin`

1. run like `cloc-git https://github.com/evalEmpire/perl5i.git`