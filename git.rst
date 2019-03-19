git
===

git remote add with other SSH port (source: https://stackoverflow.com/a/3596272/5350059)
========================================================================================
::

    git remote add origin ssh://user@host:1234/srv/git/example

check if directory is git repository without having to cd into it (source: https://stackoverflow.com/a/39518382/5350059)
=========================================================================================================================
::
    	git -C $dir_path rev-parse

using a git command inside a cron job while using ssh key
========================================================================================================
::

    #add those line at the top of script
    export SSH_AGENT_PID=`ps -a | grep ssh-agent | grep -o -e [0-9][0-9][0-9][0-9]`
    export SSH_AUTH_SOCK=`find /tmp/ -path '*keyring-*' -name '*ssh*' -print 2>/dev/null`

    (source: https://stackoverflow.com/a/16580506)

make vim git default editor
---------------------------
::

    git config --global core.editor "vim"

(source: https://stackoverflow.com/a/2596835/5350059)

git file location linux
-----------------------
::

    git config --global -e
    git config --system -e
    git config --local -e

(source: https://stackoverflow.com/a/23134785/5350059)

git commit and push without output
----------------------------------
::

    git commit --quiet
    git push --quiet

(source: https://stackoverflow.com/a/8943761/5350059)

get the current branch name in git
----------------------------------
::

    git rev-parse --abbrev-ref HEAD | grep -v ^HEAD$ || git rev-parse HEAD

(source: https://stackoverflow.com/a/46798693/5350059)
