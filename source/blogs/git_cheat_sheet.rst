Git Cheat Sheet
===============
`< Blog <../blog.html>`_

A quick reference to Git.

Created on: 2019-03-19

.. warning:: under heavy construction and not well organized

git remote add with other SSH port
----------------------------------
::

    git remote add origin ssh://user@host:1234/srv/git/example

(source: https://stackoverflow.com/a/3596272/5350059)


check if directory is git repository without having to cd into it
-----------------------------------------------------------------
::
    	git -C $dir_path rev-parse

(source: https://stackoverflow.com/a/39518382/5350059)

using a git command inside a cron job while using ssh key
---------------------------------------------------------
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

set proxy
---------
::

    git config --global http.proxy http://proxyuser:proxypwd@proxy.server.com:8080

change proxyuser to your proxy user
change proxypwd to your proxy password
change proxy.server.com to the URL of your proxy server
change 8080 to the proxy port configured on your proxy server

to get current proxy settings::

    git config --global --get http.proxy

to unset proxy::

    git config --global --unset http.proxy

(source: https://stackoverflow.com/a/19213999)

Changing author info
--------------------
to change the author info ie. name and email we need to use the `git fil` command. First save the following to a file.::

    #!/bin/sh

    git filter-branch --env-filter '

    OLD_EMAIL="your-old-email@example.com"
    CORRECT_NAME="Your Correct Name"
    CORRECT_EMAIL="your-correct-email@example.com"

    if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
    then
        export GIT_COMMITTER_NAME="$CORRECT_NAME"
        export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
    fi
    if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
    then
        export GIT_AUTHOR_NAME="$CORRECT_NAME"
        export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
    fi
    ' --tag-name-filter cat -- --branches --tags

We will save this in a file named `filter_author_info.sh`. We need the modify the `OLD_EMAIL`, `CORRECT_NAME`, and `CORRECT_EMAIL` to the match our expectation. Now we will change the file permission and run the script::

    chmod +x filter_author_info.sh
    bash filter_author_info.sh

Next we will review the new Git history for errors. Push the corrected history to remote repo::

    git push --force --tags origin 'refs/heads/*'

And we are done.

(source: https://help.github.com/en/articles/changing-author-info)

commit message template
-----------------------
to set a custom commit message template::

    git config commit.template /absolute/path/to/file

    or

    git config commit.template relative-path-from-repository-root

(source: https://stackoverflow.com/a/28948582/5350059)

rename local branch
-------------------
to rename a local branch::

    git branch -m <oldname> <newname>

(source: https://stackoverflow.com/a/6591218/5350059)

hide email address from commit log with GitHub provided email
-------------------------------------------------------------
we can hide out email address from commit log by using the GitHub provided email address::

    git config --global user.email username@users.noreply.github.com

source: https://help.github.com/en/articles/setting-your-commit-email-address

undo last commit
----------------
to undo last commit::

    git reset HEAD~

Then update remote::

    git push origin master --force

source: https://stackoverflow.com/a/927386/5350059

generate patch
--------------
to generate patch and save it on a file::

    git format-patch $brach_name_or_commit_hash --stdout > $filename.patch

source: https://stackoverflow.com/a/44950939/5350059

apply patch
-----------
to apply that patch file::

    git apply --stat $filename.patch

source: https://stackoverflow.com/a/2250170/5350059

exclude files from git diff
---------------------------
to exclude files from git diff::

    git diff -- . ':(exclude)filename'

for branch::

    git diff branchname -- ':(exclude)filename'

s: https://stackoverflow.com/a/48651201/5350059

speed up git clone
------------------
unfortunately there is no way to speed up git clone like `make -j` but we can do a shallow clone::

    git clone --depth 1 $REPO

https://stackoverflow.com/a/26957305/5350059

If we want the full clone just do::

    git fetch --unshallow

https://stackoverflow.com/a/17937889/5350059


Source
------
