# Python startup file

Two critical features are missing from a standard Python interactive
interpreter: 1) auto-completion, 2) a stored history file of
commands that can be shared between sessions. Plus, it would be nice to have
3) a custom prompt and 4) modules that are used often to be automatically
imported.

The way to achieve all this is to store the commands that you want to be
executed at the beginning of each session in `~/.pystartup`, and set an
environment variable to point to it. In bash,

    export PYTHONSTARTUP=/home/user/.pystartup

Note that `PYTHONSTARTUP` does not expand `~`, so you have to put in the
full path to your home directory.

Here is mine:

    import os
    import sys
    import atexit

    # Import the most used modules for convenience
    import re
    import json
    import datetime
    from bson.objectid import ObjectId

    # Tab auto-completion
    try:
        import readline
    except ImportError:
        print "Module readline not available."
    else:
        import rlcompleter
        if 'libedit' in readline.__doc__:
            readline.parse_and_bind("bind ^I rl_complete")
        else:
            readline.parse_and_bind("tab: complete")

    # Custom prompt to remind me whether I'm working on a production or
    # a development machine
    sys.ps1 = '[\x01\033[92m\x02dev\x01\033[0m\x02] >>> '

    # Command history
    historyPath = os.path.expanduser("~/.pyhistory")

    def save_history(historyPath=historyPath):
        import readline
        readline.write_history_file(historyPath)

    if os.path.exists(historyPath):
        readline.read_history_file(historyPath)

    atexit.register(save_history)

