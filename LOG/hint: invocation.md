hint: invocation.
Enumerating objects: 5, done.                                                                                                                                                                                          05:57:02 [58/143]
Counting objects: 100% (5/5), done.
Delta compression using up to 11 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 342 bytes | 342.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To github.com:GowthamAnbu/obsidian-v0.git
   e8e4840..38dbeb0  master -> master
updating local tracking ref 'refs/remotes/origin/master'
➜  obsidian-v0 git:(master) git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
➜  obsidian-v0 git:(master) git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   "\342\231\276\357\270\217\360\237\214\200.md"

no changes added to commit (use "git add" and/or "git commit -a")
➜  obsidian-v0 git:(master) ✗ git add . && git commit
[master 70054b7] NOW multiple level illusion of time
 1 file changed, 5 insertions(+), 1 deletion(-)
➜  obsidian-v0 git:(master) git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
➜  obsidian-v0 git:(master) git log
➜  obsidian-v0 git:(master) git show HEAD
➜  obsidian-v0 git:(master) git show HEAD
➜  obsidian-v0 git:(master) git pull origin master
remote: Enumerating objects: 37, done.
remote: Counting objects: 100% (37/37), done.
remote: Compressing objects: 100% (33/33), done.
remote: Total 34 (delta 21), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (34/34), 11.74 KiB | 308.00 KiB/s, done.
From github.com:GowthamAnbu/obsidian-v0
 * branch            master     -> FETCH_HEAD
   38dbeb0..76edac8  master     -> origin/master
hint: You have divergent branches and need to specify how to reconcile them.
hint: You can do so by running one of the following commands sometime before
hint: your next pull:
hint:
hint:   git config pull.rebase false  # merge
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
hint:
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per
hint: invocation.
fatal: Need to specify how to reconcile divergent branches.
➜  obsidian-v0 git:(master) git status
On branch master
Your branch and 'origin/master' have diverged,
and have 1 and 11 different commits each, respectively.
  (use "git pull" if you want to integrate the remote branch with yours)

nothing to commit, working tree clean
➜  obsidian-v0 git:(master) git pull origin master --rebase false
fatal: couldn't find remote ref false
➜  obsidian-v0 git:(master) git pull origin master --rebase=false
From github.com:GowthamAnbu/obsidian-v0
 * branch            master     -> FETCH_HEAD
Auto-merging ♾️🌀.md
CONFLICT (content): Merge conflict in ♾️🌀.md
Automatic merge failed; fix conflicts and then commit the result.
➜  obsidian-v0 git:(master) ✗ git status
On branch master
Your branch and 'origin/master' have diverged,
and have 1 and 11 different commits each, respectively.
  (use "git pull" if you want to integrate the remote branch with yours)

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Changes to be committed:
        new file:   LOG/.gitkeep
        modified:   narrare.md

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   "\342\231\276\357\270\217\360\237\214\200.md"

➜  obsidian-v0 git:(master) ✗ git status
On branch master
Your branch and 'origin/master' have diverged,
and have 1 and 11 different commits each, respectively.
  (use "git pull" if you want to integrate the remote branch with yours)

All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:
        new file:   LOG/.gitkeep
        modified:   narrare.md
        modified:   "\342\231\276\357\270\217\360\237\214\200.md"

➜  obsidian-v0 git:(master) ✗ git status
On branch master
Your branch and 'origin/master' have diverged,
and have 1 and 11 different commits each, respectively.
  (use "git pull" if you want to integrate the remote branch with yours)

All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:
        new file:   LOG/.gitkeep
        modified:   narrare.md
        modified:   "\342\231\276\357\270\217\360\237\214\200.md"

➜  obsidian-v0 git:(master) ✗ git commit
[master cd23a16] Merge branch 'master' of github.com:GowthamAnbu/obsidian-v0
➜  obsidian-v0 git:(master)