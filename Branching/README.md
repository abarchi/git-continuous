## Branching

> Summary of this chapter : 

	..........

* Create a branch
* Switch branches
* Merge branches
* Delete branches
* Work in parallel
* Resolve a merge conflict
* Rebase a branch

### Create a branch

Create a new directory and initialize a Git repository. We are going to create a directory named "awesome-tutorial".

```sh
$ mkdir awesome-tutorial
$ cd awesome-tutorial
$ git init
Initialized empty Git repository in /Users/eguchi/Desktop/tutorial/.git/
```

Create a new file named "myfile.txt" in the tutorial directory and commit.

I let you try to do the commit ;)
Choose a nice commit message !

Use the branch command with a name to create a new branch with that name.

```sh
$ git branch myawesome-branch
```

If you wanna see your local branches, do : 

```sh
$ git branch
```

If you wanna see your local and remote branches, do :

```sh
$ git branch -avv
```
You wanna know what each flag means ? 
**RTFM !**

### Switch branches

To switch branch, use :

```sh
$ git checkout <branch>
$ git checkout myawesome-branch
```

> NOTE :
> By passing in the -b option when executing the checkout command, a new branch will be created and you will be switched over thereafter.

```sh
$ git checkout -b <branch>
```

Now that you are on your awesome branch, let's add this bold text in myfile.txt : 
"**add: Register a change in an index**"

```
Git commands even a monkey can understand
add: Register a change in an index
```

I let you commit your changes ;)

### Merge branches

NOW let's merge myawesome-branch with master, here comes the command for merging branches : 

```sh
$ git merge <branch>
```

And with this command, the specified commit will be merged to the current active branch.

```sh
$ git merge <commit>
```

To merge commits into the master branch, let's now switch over to the master branch.

```sh
$ git checkout master
Switched to branch 'master' 
```

Before merging, check the content of the myfile.txt and see by yourself the state of your file in each branches.
As you see the change added on "myawesome-branch" described in the previous page isn't included in myfile.txt on master branch.

Now let's do :

```sh
$ git merge myawesome-branch
Updating 1257027..b2b23c4
Fast-forward
myfile.txt | 1 +
1 files changed, 1 insertions(+), 0 deletions(-)
```

After your merge, let's see myfile.txt in the master branch.
What do you notice ?

### Delete branches

Did you successfully merged with "master" ?
Perfect, so now we can remove "myawesome-branch".
Run the following command to delete "myawesome-branch".

```sh
$ git branch -d myawesome-branch
Deleted branch issue1 (was b2b23c4).
```

> You can also use -D, it combines -d (--delete) and -f (--force)

Then you can verify that your branch has been deleted, do you know what command to type ?
I let you search. Google is your friend.

### Work in parallel

Let's work in parallel :D

Create 2 branches :

```sh
$ git branch my-issue-2
$ git branch my-issue-3
$ git checkout my-issue-2
Switched to branch 'my-issue-2'
$ git branch -avv
* my-issue-2
  my-issue-3
  master 
```

Add bold text in your file myfile.txt :

**commit: Save the status of an index**

```
Git commands even a monkey can understand
add: Register a change in an index
commit: Save the status of an index
```

Commit your changes ;)
Now switch to my-issue-3.

```sh
$ git checkout my-issue-3
Switched to branch 'my-issue-3'
```
my-issue-3 has the same commit history than master.

Add the bold text below to myfile.txt and commit the change :

**pull: Obtain the content of the remote repository**

```
Git commands even a monkey can understand
add: Register a change in an index
pull: Obtain the content of the remote repository
```

Commit your changes.
**We have now added two different line of texts to two different branches in parallel.**

### Resolve a merge conflict

Let's merge "my-issue-2" and "my-issue-3" into master.

>NOTICE : 
> Check Fast-forward and non Fast-forward merge state.
> "git merge –no-ff" : The “no-fast-forward” merge option preserves the branch history and creates a merge commit, this is what happens when you merge and there is a conflict.
> A perfect merge without conflict is made in Fast-forword state.

Switch to master and merge "my-issue-2" with it.

```sh
$ git checkout master
Switched to branch 'master'
$ git merge my-issue-2
Updating b2b23c4..8f7aa27
Fast-forward
myfile.txt | 2 ++
 1 files changed, 2 insertions(+), 0 deletions(-)
```

Look at your git logs and see if "my-issue-2" branch history commit still there or not ? ;)

Now let's merge "my-issue-3" into "master".

```sh
$ git merge my-issue-3
Auto-merging myfile.txt
CONFLICT (content): Merge conflict in myfile.txt
Automatic merge failed; fix conflicts and then commit the result.
```

Resolve the conflict :)

Are you finish ?

Now you can commit your changes to resolve the conflict and you're done.

Look at your git logs and see if "my-issue-3" branch history commit still there or not ? ;)

### Rebase a branch

**Another approach we can take to integrate "my-issue-3" branch into the master branch is by using the rebase command.**

Undo merge "my-issue-3" into "master".

```sh
 $ git reset --hard HEAD~
```

And switch over to "my-issue-3" branch and rebase onto the master branch.

```sh
$ git checkout my-issue-3
Switched to branch 'my-issue-3'
$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: append description of the pull command
Using index info to reconstruct a base tree...
:13: new blank line at EOF.
+
warning: 1 line adds whitespace errors.
Falling back to patching base and 3-way merge...
Auto-merging myfile.txt
CONFLICT (content): Merge conflict in myfile.txt
Failed to merge in the changes.
Patch failed at 0001 append description of the pull command

When you have resolved this problem run "git rebase --continue".
If you would prefer to skip this patch, instead run "git rebase --skip".
To check out the original branch and stop rebasing run "git rebase --abort".
```

When a conflict occurs during the rebase, you will have to resolve it **immediately** in order to resume the rebase operation and don't commit any new changes while the rebase process".

Resolve the conflict.

When it's done you can resume rebase with the --continue option.
If you want to rollback, you can use the --abort option.

```sh
$ git add myfile.txt
$ git rebase --continue
Applying: append description of the pull command 
```

With the "my-issue-3" branch rebased onto "master", we can now issue a **fast-forward merge**.

Switch over to the master branch and merge "issue3" with "master".

```sh
$ git checkout master
Switched to branch 'master'
$ git merge my-issue-3
Updating 8f7aa27..96a0ff0
Fast-forward
myfile.txt | 1 +
 1 files changed, 1 insertions(+), 0 deletions(-)
```

Go see myfile.txt and check if the content is the same as the non fast-forward merge from the last merge.

You're done. Congratulation :D
