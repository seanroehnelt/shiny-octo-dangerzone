This repo (RepoA) was created to demenstrate an issue I ran into after using git to merge a second repo (RepoB) into a specific subdirectory of a primary repo (RepoA) using Git.

**RepoA** = A new Git repo created with a single file. This file.

**RepoB** = An existing repo on Github.com (https://github.com/BradLarson/GPUImage.git) with a useful amount of history to demonstrate the issue described above.


**Example one; as described in the git book/manual @ (**http://git-scm.com/book/ch6-7.html**)**

    ~ ❯ mkdir RepoA
    ~ ❯ cd RepoA 
    RepoA ❯ ls
    RepoA ❯ git init
    Initialized empty Git repository in /Users/sean/RepoA/.git/
    RepoA git:master ❯ mate README.md 
    RepoA git:master ❯ git add README.md 
    RepoA git:master ❯ git commit -m "Initial commit"
    [master (root-commit) 341d63f] Initial commit
     1 file changed, 3 insertions(+)
     create mode 100644 README.md

    RepoA git:master ❯ git log README.md

    commit 341d63fb5f5417e42892f492e25af1b2ada6b00b
    Author: Sean Roehnelt <s@aro.com>
    Date:   Thu Dec 6 10:00:15 2012 -0800

        Initial commit

    RepoA git:master ❯ git remote add -f RepoB https://github.com/BradLarson/GPUImage.git
    Updating RepoB
    warning: no common commits
    remote: Counting objects: 5310, done.
    remote: Compressing objects: 100% (1473/1473), done.
    remote: Total 5310 (delta 3951), reused 4928 (delta 3634)
    Receiving objects: 100% (5310/5310), 8.64 MiB | 2.54 MiB/s, done.
    Resolving deltas: 100% (3951/3951), done.
    From https://github.com/BradLarson/GPUImage
     * [new branch]      master     -> RepoB/master


**Example two; as described on github.com @ (**https://help.github.com/articles/working-with-subtree-merge**)**

    ~ ❯ mkdir RepoA
    ~ ❯ cd RepoA 
    RepoA ❯ ls
    RepoA ❯ git init
    Initialized empty Git repository in /Users/sean/RepoA/.git/
    RepoA git:master ❯ mate README.md 
    RepoA git:master ❯ git add README.md 
    RepoA git:master ❯ git commit -m "Initial commit"
    [master (root-commit) 341d63f] Initial commit
     1 file changed, 3 insertions(+)
     create mode 100644 README.md
    
    RepoA git:master ❯ git log README.md
    
    commit 341d63fb5f5417e42892f492e25af1b2ada6b00b
    Author: Sean Roehnelt <s@aro.com>
    Date:   Thu Dec 6 10:00:15 2012 -0800
    
        Initial commit
    
    RepoA git:master ❯ git remote add -f RepoB https://github.com/BradLarson/GPUImage.git
    Updating RepoB
    warning: no common commits
    remote: Counting objects: 5310, done.
    remote: Compressing objects: 100% (1473/1473), done.
    remote: Total 5310 (delta 3951), reused 4928 (delta 3634)
    Receiving objects: 100% (5310/5310), 8.64 MiB | 2.54 MiB/s, done.
    Resolving deltas: 100% (3951/3951), done.
    From https://github.com/BradLarson/GPUImage
     * [new branch]      master     -> RepoB/master

     