# Running scp through an ssh tunnel

If you want to copy a file from a remote machine **R** to the local machine
**L** (or vice versa) but the remote machine **R** is only accessible from a
gate machine **G**, the solution is to use ssh port forwarding and scp directly
from **R** to **L** through **G**. Here are the steps (all to be run on **L**):

1. Establish SSH tunnel. Pick a temporary port between 1024 and 32768 (1234 in
this example). Port 22 will be used by scp. Adding `cat -` at the end will keep
it running while you are connected to **G**:

        $ ssh -L 1234:<address of R, known to G>:22 <user at G>@<address of G> cat -

2. Open another terminal and check your localhost address:

        $ cat /etc/hosts
        127.0.0.1       localhosts

3. To scp the file, use the above port on **L** (not the remote machine
**R**) and the user name on remote machine **R**, and the command will be sent
to **R**:

        $ scp -P 1234 <user at R>@127.0.0.1:/path/to/file file-name-to-be-copied