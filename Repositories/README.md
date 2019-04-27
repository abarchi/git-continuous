## Repositories

> Summary of this chapter : 

	..........

* Push to a remote repository
* Clone a remote repository
* Push from a cloned repository
* Pull from a repository
* Make a conflict
* Resolve a conflict

### Push to a remote repository

We will register a remote repository name as "origin".
To add a remote repository, use the "remote" command. is used as an alias of a remote repository, followed by with the URL of the remote repository.

```sh
$ git remote add <*URL of the remote repository*>
$ git remote add origin https://[your_space_id].backlogtool.com/git/[your_project_key]/tutorial.git
```

[!!!!!!!! Ajoute un exemple plus concret de git remote add + une meilleur explication de la branche remote !!!!!!!!]

To push changes to the remote repository, use the "push" command.

```sh
$ git push -u origin master
Username: <username>
Password: <password>
Counting objects: 3, done. Writing objects: 100% (3/3), 245 bytes, done.
Total 3 (delta 0), reused 0 (delta 0) To https://monkey.backlogtool.com/git/BLGGIT/tutorial.git * [new branch] master -> master 
```

> TIP : 
> RTFM about git push

```sh
This might *help* you ;)

git push --help *OR* man git push
```

### Clone a remote repository

Use the "clone" command to copy a remote repository.
Substitute with the remote repository URL and with the new directory name in which the remote contents will be placed.

```sh
$ git clone https://monkey.backlogtool.com/git/BLGGIT/tutorial.git tutorial2
Cloning into 'tutorial2'... 
Username: <username>
Password: <password>
remote: Counting objects: 3, done. remote: Total 3 (delta 0), reused 0 (delta 0) Unpacking objects: 100% (3/3), done.
```

To verify that the cloning has been executed successfully, check that the following line is contained within sample.txt of the newly cloned "tutorial 2" directory.

You should see this line :
" Git commands even a monkey can understand "

### Push from a cloned repository

Add the bold text below to "sample.txt" in the newly cloned directory and commit the change.

```
Git commands even a monkey can understand
**add: Register a change in an index**
```

Then : 

```sh
$ git add sample.txt
$ git commit -m "append description of the add command"
[master 1ef5c8c] append description of the add command
1 files changed, 1 insertions(+), 1 deletions(-)
```

Now, let's push this new commit to the remote repository.

```sh
$ git push
Username: <username>
Password: <password>
Counting objects: 5, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 351 bytes, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://monkey.backlogtool.com/git/BLGGIT/tutorial.git
    486789c..1ef5c8c master -> master 
```

### Pull from a repository

Now that our remote repository is up to date with the changes from "tutorial2", let's pull the change and synchronize our initial repository directory, "tutorial".

To execute a pull, use the "pull" command. If you do not include the repository name, the pull will be executed on the repository under the alias of "origin".

```sh
$ git pull origin master
Username: <username>
Password: <password>
From https://monkey.backlogtool.com/git/BLGGIT/tutorial.git
* branch master -> FETCH_HEAD
Updating ac56e47..3da09c1
Fast-forward
sample.txt | 1 +
1 files changed, 1 insertions(+), 0 deletions(-) 
```

Let's verify that the history is updated with the "log" command.

```sh
$ git log
commit 3da09c1134a41f2bee854a413916e4ebcae7318d
Author: eguchi
Date: Thu Jul 12 18:02:45 2012 +0900

append description of the add command

commit ac56e474afbbe1eab9ebce5b3ab48ac4c73ad60e
Author: eguchi
Date: Thu Jul 12 18:00:21 2012 +0900

    first commit 
```

Let's verify and open your sample.txt file, you should see : 

```
Git commands even a monkey can understand
add: Register a change in an index 
```

### Make a conflict

Open the "sample.txt" file in the "tutorial" directory. 
Add the bold text below to the file and commit.

```sh
$ cd ../tutorial
$ vim sample.txt

Git commands even a monkey can understand
add: Register a change in an index
**commit: Save the status of an index**
```

So let's do :

```sh
$ git add sample.txt
$ git commit -m "append description of the commit command"
[master 95f15c9] append description of the commit command
 1 files changed, 1 insertions(+), 0 deletions(-) 
```

Open the "sample.txt" file in the "tutorial2" directory.
Add the bold text below to the file and commit.

```
Git commands even a monkey can understand
add: Register a change in an index
**pull: Obtain the content of the remote repository**
```

Let's do it again : 

```sh
$ git add sample.txt
$ git commit -m "append description of the pull command"
[master 4c01823] append description of the pull command
 1 files changed, 1 insertions(+), 0 deletions(-) 
```

Now push the change from "tutorial2" to the remote repository.

```sh
$ git push
Username: <username>
Password: <password>
Counting objects: 5, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 391 bytes, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://monkey.backlogtool.com/git/BLGGIT/tutorial.git
   3da09c1..4c01823 master -> master 
```

Now, we are going to push the commit from our "tutorial" repository to the remote repository.

```sh
$ git push
Username: <username>
Password: <password>
To https://monkey.backlogtool.com/git/BLGGIT/tutorial.git
! [rejected] master -> master (non-fast-forward)
error: failed to push some refs to 'https://monkey.backlogtool.com/git/BLGGIT/tutorial.git'
To prevent you from losing history, non-fast-forward updates were rejected
Merge the remote changes (e.g. 'git pull') before pushing again. See the
'Note about fast-forwards' section of 'git push --help' for details.
```

**As you can see, Git will raise a conflict and reject your push !**

### Resolve a conflict


To proceed with pushing the change to the remote repository, we will have to manually resolve the conflict. 
Let's execute a pull to acquire the most recent change set from the remote repository.

So let's do : 

```sh
$ git pull origin master
Username:
Password:
remote: Counting objects: 5, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (3/3), done.
From https://monkey.backlogtool.com/git/BLGGIT/tutorial.git
* branch master -> FETCH_HEAD
Auto-merging sample.txt
CONFLICT (content): Merge conflict in sample.txt
Automatic merge failed; fix conflicts and then commit the result.
```

Open your sample.txt and let's see the conflict : 

```
Git commands even a monkey can understand
add: Register a change in an index
<<<<<<< HEAD
commit: Save the status of an index
=======
pull: Obtain the content of the remote repository
>>>>>>> 17c860612953c0f9d88f313c8dfbf7d858e02e91 
```

Here we see that there is a conflict between the commit line and the pull line.
Are you a git warrior ?
Resolve the conflict ! :)

Are you done editing your file ?
If yes, don't forget to commit your changes !

```sh
$ git add sample.txt
$ git commit -m "merge"
[master d845b81] merge 
```

YEAHHHH ! Now we are up to date with the latest change(s) from the remote repository.

Let's verify the accuracy of the repository history using the "log" command : 

```sh
$ git log --graph --oneline
* d845b81 merge
|\
| * 4c01823 append description of the pull command
* | 95f15c9 append description of the commit command
|/
* 3da09c1 append description of the add command
* ac56e47 first commit 
```
> This indicates that the two histories have been merged successfully with a new merge commit.

And now we can safely push without fear to the remote repository.
