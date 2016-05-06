# Filesystem navigation

In order to accelerate navigation to deep directories, there is a manual
solution that can come in handy. It comes down to storing symbolic links in a
hidden directory (e.g., `~/.marks`). It consists of four shell functions: `jump`,
`mark`, `unmark`, and `marks`, and they look like this:

    export MARKPATH=$HOME/.marks
    function jump {
        cd -P "$MARKPATH/$1" 2>/dev/null || echo "No such mark: $1"
    }
    function mark {
        mkdir -p "$MARKPATH"; ln -s "$(pwd)" "$MARKPATH/$1"
    }
    function unmark {
        rm -i "$MARKPATH/$1"
    }
    function marks {
        ls -l "$MARKPATH" | sed 's/  / /g' | cut -d' ' -f9- | sed 's/ -/\t-/g' && echo
    }
    _completemarks() {
      local curw=${COMP_WORDS[COMP_CWORD]}
      local wordlist=$(find $MARKPATH -type l -printf "%f\n")
      COMPREPLY=($(compgen -W '${wordlist[@]}' -- "$curw"))
      return 0
    }
    complete -F _completemarks jump unmark

These can just be added to the shell config file (e.g. `.bashrc`). To add a new
bookmark, cd into the directory and mark it with a name:

    $ cd ~/some/very/deep/often-used/directory
    $ mark deep

This adds a symbolic link named `deep` to the directory `~/.marks`. To jump to
this directory, type the following from any place in the filesystem:

    $ jump deep

To remove the bookmark (i.e., the symbolic link), type:

    $ unmark deep

You can view all marks by typing:

    $ marks
    deep    -> /home/johndoe/some/very/deep/often-used/directory
    foo     -> /usr/bin/foo/bar

Thanks to the last function, `_completemarks`, autocompletion is enabled for
`jump` and `unmark`.

