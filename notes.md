
Notes on Git & GitHub
---------------------

#### Config file

    ./.git/config

#### Clone from github 

    # use SSH avoiding password prompt
    git clone git@github.com:frozen-flame/gitstart.git

#### Update from local to remote

    git push

#### Update from remote to local

    git pull origin master

=======================================

#### Frequent commands

    git add FILENAME

    git status
    git log

    git commit -m 'MESSAGE'
    git commit -a -m 'MESSAGE'

    git reflog
    git reset --hard HASH

=======================================

#### Config username and email

    # repo-wise (saved to .git/config)
    git config user.name frozflame
    git config user.email lendoli@163.com
    
    # user-wise (saved to ~/.gitconfig)
    git config --global user.name frozflame
    git config --global user.email lendoli@163.com

=======================================

#### Switch from HTTPS to SSH

    git remote rm origin
    git remote add origin git@github.com:yuquan0821/demo.git
    git push origin 


