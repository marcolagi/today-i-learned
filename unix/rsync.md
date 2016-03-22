# rsync with identity file

When in need to make periodic backups on a remote server to be accessed through
`ssh` keys, `rsync` picks by default `~/.ssh/id_rsa`. If the indentity file is
something else, you'll get `Permission denied (publickey)`. One has to specify
the exact `ssh` command via the `-e` option:

    rsync -avz -e "ssh -i [LOCAL_PATH_TO_KEY]" [LOCAL_DIR] [USER]@[TARGET]:[REMOTE_DIR]

The absolute path to the identity key file is necessary in this case.




