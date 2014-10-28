
Git Rename 
----------

Clumsy way

    mv oldname newname
    git rm oldname
    git add newname

Easy way

    git mv oldname newname

Both works, and git can follow the history before renaming in both cases

    git log --follow newname
