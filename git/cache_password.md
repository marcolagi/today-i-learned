# Cache GitHub password

If you're cloning GitHub repositories using HTTPS on a Linux machine, you can
use a credential helper to tell git to remember your username and
password every time it talks to GitHub.

Turn on the credential helper so that git will save your password in memory for
some time with

    git config --global credential.helper cache

By default, git will cache your password for 15 minutes. To change the default
password cache timeout (setting is in seconds),

    git config --global credential.helper 'cache --timeout=3600'