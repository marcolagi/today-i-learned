# Show tracked files

In order to show a list of the files that are being tracked in a repository,
for example under the branch `master`, the command is:

    git ls-files

or

    git ls-tree -r master --name-only

For the current branch, instead, use `-r HEAD`