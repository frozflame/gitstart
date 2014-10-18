
Diff
----

Examples

    git diff origin/master master

You have to `commit` before you can see the difference.

Just change the file will not bring you to that difference,
since it is not considered as part of the master branch of current repo.

Note

`remotes/origin/master` and `origin/master` refer to the same thing.

================================

Find differences of between to commits of a perticular file

    git diff HEAD^^ HEAD main.c

Read from [this][1] stackoverflow post.

[1]: http://stackoverflow.com/questions/3338126/git-how-to-diff-the-same-file-between-two-different-commits-on-the-same-branch

