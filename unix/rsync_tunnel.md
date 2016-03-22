# Running rsync through an ssh tunnel

When in need to make periodic backups on a remote server to be accessed through
an `ssh` tunnel, and all machines can only be accessed through identity keys,
one can specify the exact `ssh` command via the `-e` option:

    rsync -avz -e "ssh -i [LOCAL_PATH_TO_KEY] [USER]@[PROXY] ssh -i [PROXY_PATH_TO_KEY]" [LOCAL_DIR] [USER]@[TARGET]:[REMOTE_DIR]

The absolute paths to the identity key files are necessary in this case.




