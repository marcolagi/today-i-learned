# Add existing project to GitHub

Here are the steps:

1. Create a new repo on GitHub. To avoid errors, do not initialize with README,
license, or gitignore files.

2. Go to your local project and initialize that directory as a git repo:

        $ git init

3. Add all files to the new local repository (this stages them for the first
commit) and commit:

        $ git add .; git commit -m "First commit"

4. At the top of your GitHub repo's **Quick Setup** page, click the copy symbol
to copy the remote repository URL.

5. Add the URL for the remote repository where your local repository will be
pushed.

        $ git remote add origin [remote repo URL]
        $ git remote -v

6. Push the changes in your local repository to GitHub.

        $ git push origin master