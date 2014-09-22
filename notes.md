
clone from github (use SSH avoiding password prompt)

    git clone git@github.com:frozen-flame/gitstart.git

# update from local to remote

    git push

# update from remote to local
git pull origin master


--

git add FILENAME

git status
git log
git reflog
git reset --hard HASH

git commit -m 'MESSAGE'
git commit -a -m 'MESSAGE'

--

git config user.name frozen-flame
git config user.email lendoli@163.com

--

Avoid username/password prompt:

1. git remote rm origin
2. git remote add origin git@github.com:yuquan0821/demo.git
3. git push origin 


