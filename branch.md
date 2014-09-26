
Branch
=======

Create and switch to new branch `hotfix`

    $ git checkout -b hotfix

which is equivolent to 

    $ git branch hotfix
    $ git checkout hotfix

-------

Switch between branches

    $ git checkout master
    $ git checkout hotfix

Show available branches (and current branch)

    $ git branch
    $ git branch -v 

-------

Merge `hotfix` to `master`

    $ git checkout master
    $ git merge hotfix

Delete `hotfix` then

    $ git branch -d hotfix

-------





