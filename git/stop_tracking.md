# Stop tracking files

When you have a file that was being tracked at one time by git, but you want
git to stop tracking it, the first step is adding it to `.gitignore`.

However, you'll notice that the file keeps showing up in `git status` after
it's edited. This is because `.gitignore` prevents untracked files from
being added to the set of tracked files, but git continues to track any
files that are already being tracked.

In order to force git to completely fuggedaboutit, you need to remove it from
the index, or rebuild the index entirely. This can be achieved with:

    git rm -r --cached .
    git add .

Of course there's always the ghetto solution: move the file out, commit, then
move it back in.