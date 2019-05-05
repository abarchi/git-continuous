**!CAUTION!**

> NOTICE :
> With this chapter I recommand you to create your own repository with your own commits and messages related, because it's a good exercise and it will help us to do more complexe command with git. 
> Create also a fake text file to test and create a nice log history of your code changes.

## Rewriting history

* Commit --amend
* Revert
* Reset
* Cherry pick
* Squash commits with rebase
* Change commits using rebase
* Merge --squash

Let's rewrite the first commit in the history log.

### Commit --amend
So when you got your repository, your branch master and few commits you can log your commits : 

It looks like something like this : 

```sh
$ git log
commit 326fc9f70d022afdd31b0072dbbae003783d77ed
Author: yourname <yourname@yourmail.com>
Date: Mon Jul 16 23:17:56 2012 +0900

    append description of the add command

commit 48eec1ddf73a7fb508ef664efd6b3d873631742f Author: yourname <yourname@yourmail.com> Date: Mon Jul 16 23:16:14 2012 +0900

    first commit
```

Add text in your fake file and git add your changes.
But imagine you want to change the message of your commit that your are working on and you approved with git add, you can use --amend option.

```sh
$ git commit --amend
```

Change your message and commit.
Log your history commits and your commit message should now be updated.

### Revert

So when you got your repository, your branch master and few commits you can log your commits :

We are going to undo the "append description of the pull command" commit or your last commit using the "revert" command.

Examine the history log using the log command.

Open your fake text file and verify the state of your modification.
It should look like this for example :

```sh
Git commands even a monkey can understand 
add: Register a change in an index 
commit: Save the status of an index 
pull: Obtain the content of the remote repository
```

Let's undo the latest HEAD, so your last commit message and revert it with the "git revert" command : 

```sh
$ git revert HEAD 
[master d47bb1d] 
Revert "append description of the pull command"
 1 files changed, 1 insertions(+), 2 deletions(-)
```

Open your fake text file again. If the above procedure has been done correctly, the last modification/commit you added should no longer exist.
You can for example revert your last commit you changed with "commit --amend" to come back to the previous state.

Git log your history and see by yourself ;)

### Reset

So when you got your repository, your branch master and few commits you can log your commits :

Here we are going to undo the previous two commits using the reset command.

Open your fake text file and verify your modification state.
Examine your log histrory and look where your HEAD is and step back 2 commits and "git reset" on it.

```sh
$ git reset --hard HEAD~~ 
HEAD is now at 326fc9f append description of the add command  
```

> NOTE :
> The 2 last "~" after HEAD means the 2 last commit from where your HEAD is.

If you now look your fake file text you will see your 2 last modification deleted.
You can verify that with a nice "git log" command.

> NOTE : 
> ORIG_HEAD points to the original commit before reset actually takes place.
> This may come in handy especially when you accidentally issue a reset.
> You can restore the previous history by executing a reset to ORIG_HEAD.

```sh
$ git reset --hard ORIG_HEAD
```

If you look you can undo reset, **but don't commit anything because you will disturbe the reset process !**
Your 2 commits that you reset should be back in your log history.

### Cherry pick

So when you got your repository, your branch master and few commits you can log your commits :

In this step, we are going to create a new commit in the master branch that is a copy of the commit of your last message residing on a different branch within the same repository.

First of all, create a second branch from "master" branch.

```sh
$ git branch my-cherry-pick-branch
```

> NOTE :
> Our "master" is the origin branch of our second branch.

Checkout on your second branch "my-cherry-pick-branch".

Add some commits and switch back to your master branch.

Examine your log history : 

Use the cherry-pick command and lets copy your first commit hash of your "my-cherry-pick-branch".

Your cherry-pick command should look like this : 

```sh
$ git cherry-pick <your first commit hash>
error: could not apply 99daed2... 
commit hint: after resolving the conflicts, mark the corrected paths hint: with 'git add <paths>' or 'git rm <paths>' hint: and commit the result with 'git commit' 
```

As you can see, a conflict has occurred from your fake text file.
Manually resolve it and proceed with a "git add" and a "git commit".

### Squash commits with rebase

So when you got your repository, your branch master and few commits you can log your commits :

In this step, we are going to combine your two commits into a single commit.

To do that we have to pass in interactive rebasing :

```sh
$ git rebase -i HEAD~~
```

> NOTE : 
> The 2 last "~" after HEAD means the 2 last commit from where your HEAD is.

Your default text editor should open and you will be on rebase interactive mode showing commits from HEAD to HEAD~~ as shown below.

It should look like this :

```sh
pick 9a54fd4 append description of the commit command 
pick 0d4a808 append description of the pull command 
# Rebase 326fc9f..0d4a808 onto d286baa 
# 
# Commands: 
# p, pick = use commit 
# r, reword = use commit, but edit the commit message 
# e, edit = use commit, but stop for amending 
# s, squash = use commit, but meld into previous commit 
# f, fixup = like "squash", but discard this commit's log message 
# x, exec = run command (the rest of the line) using shell 
# 
# If you remove a line here THAT COMMIT WILL BE LOST. 
# However, if you remove everything, the rebase will be aborted. 
#
```

On the second line/commit, change the word "pick" to "squash", then save and quit.

Then the editor will now prompt you to edit the commit message of this newly formed commit.

Edit the commit message, then save and quit.

And now if you log your commit references you will see the details of your rebase process : 

```sh
$ git reflog
```

### Change commit using rebase

So when you got your repository, your branch master and few commits you can log your commits :

Let's do :

```sh
$ git rebase -i HEAD~~
```

Your default text editor will open listing commits from HEAD down to HEAD~~ as shown below.

It should look like this :
```sh
pick 9a54fd4 append description of the commit command 
pick 0d4a808 append description of the pull command 
# Rebase 326fc9f..0d4a808 onto d286baa 
# 
# Commands: 
# p, pick = use commit 
# r, reword = use commit, but edit the commit message 
# e, edit = use commit, but stop for amending 
# s, squash = use commit, but meld into previous commit 
# f, fixup = like "squash", but discard this commit's log message 
# x, exec = run command (the rest of the line) using shell 
# 
# If you remove a line here THAT COMMIT WILL BE LOST. 
# However, if you remove everything, the rebase will be aborted. 
#
```

On the first line/commit, change the word "pick" to "edit", then save and quit.

```sh
Stopped at d286baa... append description of the commit command 
You can amend the commit now, with git commit --amend Once you are satisfied with your changes, run git rebase --continue 
```

Open your fake text file and make some changes.

Approve your changes and use commit --amend to make the change.

```sh
$ git add sample.txt
$ git commit --amend
```

> NOTE :
> While running a rebase on your current brach, you may run into conflicts in your changes. 
> In that case, you will want to manually resolve those conflicts, then run "add" and "rebase --continue". 
> You would only want to resolve conflicts at this point, and there is no need to issue any new commits.
>
> If you would like to stop rebasing however, you can call "rebase --abort" which will revert and exit the entire rebase process.


In cases where you specify "edit" on more than a single line when calling "git rebase -i", you will be prompted to amend each of the commits one at a time.

> NOTE :
> ORIG_HEAD points to the original commit before rebase actually takes place.
> This may come in handy especially when you accidentally issue a rebase.
> You can restore the previous history state by executing a rebase to ORIG_HEAD.

### Merge --squash

So when you got your repository, your branch master and few commits you can log your commits :

**Now, we are going to squash commits from the "issue1" branch to a single commit and merge it into the master branch !**

First of all, create a second branch named "my-awesome-feature" and create a few commits from a fake text file.

Switch over to the master branch. Execute a merge with the option --squash like below.

```sh
$ git checkout master 
Switched to branch 'master' 
$ git merge --squash issue1 
Auto-merging sample.txt CONFLICT (content): Merge conflict in sample.txt 
Squash commit -- not updating HEAD Automatic merge failed; fix conflicts and then commit the result.
```

Git detected a conflict, resolve it manually.
Commit your changes.

We now have a new commit added to the master branch which includes all of the commits in the "issue1" branch.
You can verify the new change in the revision history using the log command.

Congratulation, you finish this chapter ! :D
