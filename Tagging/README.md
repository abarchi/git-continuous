## Tagging 

> Summary of this chapter :

	..........

* Add a tag
* Delete a tag

### Add a tag

Prepare yourself : 

"Don't hesitate to create your own repository git for testing context purpose."

So, create a new directory and initialize a new empty repository.

```sh
$ mkdir tutorial
$ cd tutorial
$ git init
Initialized empty Git repository in /Users/eguchi/Desktop/tutorial/.git/
```

Touch a file named "modification.txt" and put inside this bold text.

**Git commands even a monkey can understand**

```sh
$ git add myfile.txt
$ git commit -m "first commit"
[master (root-commit) a73ae49] first commit
1 files changed, 1 insertions(+), 0 deletions(-)
 create mode 100644 myfile.txt
```

To add a lightweight tag : 

```sh
$ git tag <tagname>
```

Running tag without any parameters gives you a list of tags in this repository.

```sh
$ git tag
apple
```

Create a tag named version 0.1.

```sh
$ git tag 0.01
```

And see the log history of your commit.
**Pay attention of this command, it is not the same as the "git reflog" command which is nice for debugging !**

```sh
$ git log --decorate
commit e7978c94d2104e3e0e6e4a5b4a8467b1d2a2ba19 (HEAD, tag: 0.01, master)
Author: yourname <yourname@yourmail.com>
Date: Wed Jul 18 16:43:27 2012 +0900

    first commit
```

Let's add an annotated tag, with this command which opens the default text editor that lets you add notes to the tag : 

```sh
$ git tag -a <tagname>
```

If you want to bypass the text editor and add the note alongside the tag creation, use -am option :

```sh
$ git tag -am "Git Beginner's Guide for Dummies" 0.02
```

Passing in the -n option gives you the list of tags with their notes for this repository.

```sh
$ git tag -n
0.01 first commit
0.02 Git Beginner's Guide for Dummies 
```

### Delete a tag

To delete a tag : 

```sh
$ git tag -d <tagname>
```
