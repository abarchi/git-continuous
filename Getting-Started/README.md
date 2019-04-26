## Getting Started

> Summary of this chapter :

	.......... 

* Install git
* Default settings
* Create a repository
* Commit a file

### Install git

* Windows
  * TortoiseGit is a Windows Shell Interface to Git and based on TortoiseSVN. It's open source and can fully be build with freely available software.
  * First of all, download the TortoiseGit installer. Depending on your Windows OS, you will have to decide between the 32 bit or 64 bit version.
    * http://code.google.com/p/tortoisegit/
  * To proceed with the tutorial, you will have to install msysgit on your computer.
    * http://msysgit.github.io/
  * After installation, go to Start menu > All programs > Git > Git Bash.

* Mac
  * On a Mac, you can use a Git client called SourceTree. It is created by Atlassian and is free to use.
    * http://www.sourcetreeapp.com/
  * Download the Git installer from the Git website
    * http://git-scm.com/
* CLI
  * Check that git was installed with this command
  ```
  $ git --version 
  git version 1.7.7.5 (Apple Git-26)
  ```
> **! For the rest of this tutorial we will always use the command line !**

### Default settings

To set up the default username and e-mail address for Git that will be used to identify the person who commits the change, use this command : 

```
$ git config --global user.name "<*your git username*>"
$ git config --global user.email "<*your email related to git*>"
```

### Create a repository

```
$ mkdir tutorial

$ cd tutorial

$ git init
```

### Commit a file

Use the "status" command to confirm the status of our Git working tree and index.

```
$ vim sample.txt
Add this line to your sample.txt : "*Git commands even a monkey can understand*"
$ git status
# On branch master # # Initial commit # # Untracked files: # (use "git add ..." to include in what will be committed) # # sample.txt nothing added to commit but untracked files present (use "git add" to track)
```

You will need to add "sample.txt" to the index first in order to track its change.

> TIP : 
> Specify "." instead of individual file names, if you wish to add all of the changed files to the index.

```
$ git add <*sample.txt*> **OR** $ git add .
$ git status
# On branch master # # Initial commit # # Changes to be committed: # (use "git rm --cached ..." to unstage) # # new file: sample.txt # 
```

Now that "sample.txt" has been added to the index, we can proceed with committing the file.

```
$ git commit -m "<*Your commit message*>"
[master (root-commit) 116a286] first commit 0 files changed, 0 insertions(+), 0 deletions(-) create mode 100644 sample.txt 

$ git status 
# On branch master nothing to commit (working directory clean) 
```

We can see the newly added commit in the repository's history log with the "log" command.

```
$ git log commit 
ac56e474afbbe1eab9ebce5b3ab48ac4c73ad60e Author: eguchi Date: Thu Jul 12 18:00:21 2012 +0900 <*Your commit message*> 
```

> NOTE :
> If you prefer a GUI way of diving into the repository history, you can do so using "gitk" that is shipped along side with Git.

```
$ gitk
```
