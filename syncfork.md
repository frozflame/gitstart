
Sync fork
===========

#### from fork to upstream ####

Owner of `fork` create a `Pull Request` from the GitHub website.
Owner of `upstream` accept it to merge changes to `upstream`.

-------

#### from upstream to local fork ###

The following links will help

*   [Configuring a remote for a fork] [1]
*   [Syncing a fork] [2]

[1]: https://help.github.com/articles/configuring-a-remote-for-a-fork
[2]: https://help.github.com/articles/syncing-a-fork

Here is a cheatsheet like summary. To configure

    $ git remote -v
    $ git remote add upstream git@github.com:frozflame/gitstart.git
    $ git remote -v

To sync

    $ git fetch upstream
    $ git checkout master
    $ git merge upstream/master

-------
    

