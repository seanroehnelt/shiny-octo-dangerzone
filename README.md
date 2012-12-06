This repo (RepoA) was created to demenstrate an issue I ran into after using git to merge a second repo (RepoB) into a specific subdirectory of a primary repo (RepoA) using Git.

**RepoA** = A new Git repo created with a single file. This file.

**RepoB** = An existing repo on Github.com <https://github.com/BradLarson/GPUImage.git> with a useful amount of history to demonstrate the issue described above.

##Example one; as described on github.com @ <https://help.github.com/articles/working-with-subtree-merge>

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

    RepoA git:master ❯ git merge -s ours --no-commit RepoB/master
    Automatic merge went well; stopped before committing as requested
    
    RepoA git:master ❯ git read-tree --prefix=Frameworks/RepoB/ -u RepoB/master
    
    RepoA git:master ❯ git commit -m "Subtree merged GPUImage (https://github.com/BradLarson/GPUImage.git) at repo path 'Frameworks/RepoB'"
    [master 213259d] Subtree merged GPUImage (https://github.com/BradLarson/GPUImage.git) at repo path 'Frameworks/RepoB'
    
    RepoA git:master ❯ git remote add origin git@github.com:seanroehnelt/shiny-octo-dangerzone.git
    RepoA git:master ❯ git push -u origin master
    Host key fingerprint is [snip]
    [snip]
    Counting objects: 5317, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (1161/1161), done.
    Writing objects: 100% (5317/5317), 8.64 MiB | 267 KiB/s, done.
    Total 5317 (delta 3952), reused 5310 (delta 3951)
    To git@github.com:seanroehnelt/shiny-octo-dangerzone.git
     * [new branch]      master -> master
    Branch master set up to track remote branch master from origin.
    
    RepoA git:master ❯ git add README.md
    RepoA git:master ❯ git commit -m "Add info to README.md file in @ RepoA/README.md"
    [master f8b2568] Add info to README.md file in @ RepoA/README.md
     1 file changed, 32 insertions(+), 1 deletion(-)
    RepoA git:master ❯ git push
    [snip]
    Counting objects: 5, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (3/3), 897 bytes, done.
    Total 3 (delta 1), reused 0 (delta 0)
    To git@github.com:seanroehnelt/shiny-octo-dangerzone.git
       213259d..f8b2568  master -> master
    
    RepoA git:master ❯ cd
    ~ ❯ git clone git@github.com:seanroehnelt/shiny-octo-dangerzone.git
    Cloning into 'shiny-octo-dangerzone'...
    [snip]
    remote: Counting objects: 5317, done.
    remote: Compressing objects: 100% (1160/1160), done.
    remote: Total 5317 (delta 3952), reused 5317 (delta 3952)
    Receiving objects: 100% (5317/5317), 8.64 MiB | 2.76 MiB/s, done.
    Resolving deltas: 100% (3952/3952), done.

## PROBLEMS

    ~ ❯ cd shiny-octo-dangerzone
    shiny-octo-dangerzone git:master ❯ 
    
### `git log -- Frameworks/RepoB/License.txt`

    shiny-octo-dangerzone git:master ❯ git log -- Frameworks/RepoB/License.txt
    commit 213259db595c1b852429b20bf3c6d633f362e67d
    Merge: 341d63f 1e0e621
    Author: Sean Roehnelt <s@aro.com>
    Date:   Thu Dec 6 10:51:32 2012 -0800

        Subtree merged GPUImage (https://github.com/BradLarson/GPUImage.git) at repo path 'Frameworks/RepoB'

### `git log --follow -- Frameworks/RepoB/License.txt`
    shiny-octo-dangerzone git:master ❯ git log --follow -- Frameworks/RepoB/License.txt
    shiny-octo-dangerzone git:master ❯

### `git log --follow -- License.txt` (note: License.txt is only @ Frameworks/RepoB/License.txt)
    shiny-octo-dangerzone git:master ❯ git log --follow -- License.txt
    commit 84061527fd590d35cd3e7d2e6c4d65b7e35fe74a
    Author: Jake Gundersen <fattjake@gmail.com>
    Date:   Wed May 2 16:04:59 2012 -0600

        Replaced everything with a copy from the parent project
    
        Had some corruption I couldn't track down

    commit d1d3586732797d3ca2c41091328b6166b38974ba
    Author: Brad Larson <larson@sunsetlakesoftware.com>
    Date:   Sat Mar 31 22:42:22 2012 -0500

        Fixed the sizing issues I was having with the still photo capture, and fixed the preview input on iOS 4.0. The still camera is now functional on every device but th

    commit 7662a0bbad62d7fb5b9192f18fce5bb2f9c019bd
    Author: Brad Larson <larson@sunsetlakesoftware.com>
    Date:   Tue Feb 28 08:41:21 2012 -0600

        Fixed a couple of compilation issues with the project. Still working on the video recording.
    [more]

##Example two; as described in the git book/manual @ <http://git-scm.com/book/ch6-7.html>

    IN PROGRESS...
