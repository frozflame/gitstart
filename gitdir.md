
Observe `.git`
-------------
Directory structure after `git init`

    $ git init
    $ tree -a 
    .
    ├── .git
    │   ├── branches
    │   ├── COMMIT_EDITMSG
    │   ├── config
    │   ├── description
    │   ├── HEAD
    │   ├── hooks
    │   │   ├── applypatch-msg.sample
    │   │   ├── commit-msg.sample
    │   │   ├── post-update.sample
    │   │   ├── pre-applypatch.sample
    │   │   ├── pre-commit.sample
    │   │   ├── prepare-commit-msg.sample
    │   │   ├── pre-push.sample
    │   │   ├── pre-rebase.sample
    │   │   └── update.sample
    │   ├── info
    │   │   └── exclude
    │   ├── objects
    │   │   ├── info
    │   │   └── pack
    │   └── refs
    │       ├── heads
    │       └── tags
    └── hello.txt

Create a file and `git add`

    $ echo 'Hello World' > hello.txt
    $ git add hello.txt
    $ tree -a
    .
    ├── .git
    │   ├── branches
    │   ├── COMMIT_EDITMSG
    │   ├── config
    │   ├── description
    │   ├── HEAD
    │   ├── hooks
    │   │   ├── applypatch-msg.sample
    │   │   ├── commit-msg.sample
    │   │   ├── post-update.sample
    │   │   ├── pre-applypatch.sample
    │   │   ├── pre-commit.sample
    │   │   ├── prepare-commit-msg.sample
    │   │   ├── pre-push.sample
    │   │   ├── pre-rebase.sample
    │   │   └── update.sample
    │   ├── index
    │   ├── info
    │   │   └── exclude
    │   ├── objects
    │   │   ├── 55
    │   │   │   └── 7db03de997c86a4a028e1ebd3a1ceb225be238  **
    │   │   ├── info
    │   │   └── pack
    │   └── refs
    │       ├── heads
    │       └── tags
    └── hello.txt

Then commit

    $ git commit -m 'create hello.txt'
    $ tree -a
    .
    ├── .git
    │   ├── branches
    │   ├── COMMIT_EDITMSG
    │   ├── config
    │   ├── description
    │   ├── HEAD
    │   ├── hooks
    │   │   ├── applypatch-msg.sample
    │   │   ├── commit-msg.sample
    │   │   ├── post-update.sample
    │   │   ├── pre-applypatch.sample
    │   │   ├── pre-commit.sample
    │   │   ├── prepare-commit-msg.sample
    │   │   ├── pre-push.sample
    │   │   ├── pre-rebase.sample
    │   │   └── update.sample
    │   ├── index
    │   ├── info
    │   │   └── exclude
    │   ├── logs
    │   │   ├── HEAD
    │   │   └── refs
    │   │       └── heads
    │   │           └── master  **
    │   ├── objects
    │   │   ├── 55
    │   │   │   └── 7db03de997c86a4a028e1ebd3a1ceb225be238
    │   │   ├── 67
    │   │   │   └── ff32ef69615acd576caf292a3ad95c35e2ef7c  **
    │   │   ├── 97
    │   │   │   └── b49d4c943e3715fe30f141cc6f27a8548cee0e  **
    │   │   ├── info
    │   │   └── pack
    │   └── refs
    │       ├── heads
    │       │   └── master
    │       └── tags
    └── hello.txt


