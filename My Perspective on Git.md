# My Perspective on Git

## Git Overview

### What is Git?

* Git is a distributed version control system which means each user has a local copy of the repository and can easily be synchronized.

### What is a Git repository?

* A series of **snapshots** or **commits**.



## Getting Started

### Configuring user information and the default editor

* Use the `git config [--local | --global | --system] <key> [<value>]` command to specify or read configuration information.

```
git config --global user.email "yuxiangwang0829@gmail.com" # set
git config --global user.email # get
yuxiangwang0829@gmail.com
```

* Use the `git config --global core.editor [<editorname>]` command to specify or read your preferred Git editor.

```
git config --global core.editor sublime_text # set
git config --global core.editor # get
sublime_text
```



## Git Locations

### working tree

* A single commit's directories and files.
* You can view and edit the files of project, preparing for the next commit.

### Staging area/index

* Files that are planned for the next commit.

### Local repository

* Contains all of the commits that have been made for the project.

### Project directory

* Working tree
* Staging area
* Local repository
* **A hidden .git directory where the staging area and local repository are located.**

### Remote repository

* Contains the commits of the project.



## Create a Local Repository

* `git init` -- initialize (create) an empty repository.



## Commit to a Local Repository

* Use `git status` to view the status of files in the working tree and staging area.
* Use `git add` to add content to the staging area.
* Use the `git commit -m` command to add staged content to the local repository as a commit. You can use the `-m` flag to specify a short commit message.
* Use `git log --oneline` to view the local repository's commit history. The `--oneline` is optional.



## Push to a Remote Repository

### Remotes - git clone vs. git remote add

**If you want to begin working with the remote repository, you have two main options:**

* If have a local repository, you want to **push** to a remote repository, than you will **add** the remote repository to your local repository.
* If not have a local repository, you will **clone** the remote repository which will create a local repository that is associated with the remote repository.

### Clone a remote repository

* A clone is a local copy of a remote repository.

* A reference to the remote repository is included in the local repository. So you can synchronize the repository.
* **origin** is the default alias for the remote repository URL.
* `git clone <url/to/projectname.git> [localprojectname]` is used to create a local copy of a remote repository. The last argument (which defines the name of the directory name where the local repository is located) is optional. Cloning will create a project directory in your local computer.
* After cloning, all the commits on the remote repository will also in your local repository.
* `git remote --verbose` displays information about remote repositories associated with the local repository.

### Add a remote repository to a local repository

* `git remote add <name> <url>` command will add information about the remote repository to the local repository. The two repositories can then be synchronized using aliases instead of URL.

### Push commits to a remote repository

* All commits belong to a branch.

> A branch can be thought of as an independent line of development of the project.

* By default, there is a single branch and it is called **master**.
* `git push [-u] [<repository>] [<branch>]` writes commits for a branch from the local repository to a remote repository.
* * `<repository>` can be a name(shortcut which is often origin) or URL
  * `-u` flag is set to set up a tracking relationship between the local and remote branch
  * `[<branch>]` is the branch in the remote repository that you want to push to
  * The arguments after `git push` are all optional, because git will assume default information or use previous arguments after you have executed the first push
* A successful push synchronizes the branches on the local and remote repositories so that they they contain exactly the same commits.
* Before you run `git push` command you can use `git remote --verbose` command to ensure that your local repository has an association with the remote repository.



## Git's Graph Model

* **Git models the relationship of commits with directed acyclic graph.**
* **The arrows point at a commit's parent(s).**
* **The commits and the relationship between them is what forms the project's history.**
* **A branch occurs if a commit has more than one child.**

![branch](https://github.com/wangyuxiang0829/My-Perspective-on-Git/blob/master/pngs/branch.jpg)

* **A merge occurs when a commit has more than one parent.**

![merge](https://github.com/wangyuxiang0829/My-Perspective-on-Git/blob/master/pngs/merge.jpg)

* `git log --graph` will show you a diagram.



## Git IDs

### Git Objects

1. Commit object - A small text file
2. Annotated tag - A reference to a specific commit
3. Tree - Directories and filenames in the project
4. Blob - The content of a file in the project

### Git ID

* The name of a Git Object
* 40 - character hexadecimal string
* Also known as object ID, SHA-1, hash, and checksum

### Shortening Git IDs

* The first portion of the Git ID



## References

### Overview of references

* Commits can be associated with references
* A reference is a user-friendly name that points to:
* * a commit SHA-1 hash
  * another reference(known as a symbolic reference) (such as HEAD)
* Use references instead of SHA-1 hashes, `git show` command can show the specified commit message, such as use `git show HEAD` 
* References are stored in the .git directory

### Branch labels and HEAD

* **master** is the default name of the main branch in the repository
* **A branch label** points to the most recent commit in the branch

![label](https://github.com/wangyuxiang0829/My-Perspective-on-Git/blob/master/pngs/label.jpg)

* **Branch labels** are implemented as references
* The difference between a branch and a branch label:
* * All commits belong to the branch
  * The branch label is only at the latest commit of the branch
* **HEAD** is a reference to the current commit
* **HEAD** usually points to the branch label of the current branch

![HEAD](https://github.com/wangyuxiang0829/My-Perspective-on-Git/blob/master/pngs/HEAD.jpg)

* Only one **HEAD** per repository

### Tags

* A **tag** is a reference attached to a specified commit. It acts a user-friendly label for the commit

![tag](https://github.com/wangyuxiang0829/My-Perspective-on-Git/blob/master/pngs/tag.jpg)

* There are two types of Tags:
* * Lightweight(A simple reference to a commit much like branch label or HEAD)
  * Annotated(recommended)
  * * A full Git object that references a commit
    * Includes tag author information, tag date, tag message, the commit ID

* `git tag` - View all tags in the repository

* Tags can be used instead of branch labels or Git IDs in Git commands such as `git show v1.0`

* To tag a commit with a lightweight tag:
* * `git tag <tagname> [<commit>]`
  * `<commit>` defaults to HEAD

* To tag a commit with an annotated tag:
* * `git tag -a [-m <msg> | -F <file>] <tagname> [<commit>]`
  * `commit` default to HEAD

* `git push` does not automatically transfer tags to the remote repository
* To transfer a single tag: `git push <remote> <tagname>`
* To transfer all of your tags: `git push <remote> --tags`



## Branches

### Branch overview

* A **branch** is a set of commits starting with the most recent commit in the branch and tracing back to the project's first commit
* Fast and easy to create
* Enable experimentation
* Enable team development
* Support multiple project versions
* **Short-lived** (commonly called topic or feature branches) usually contain one small change to the project

![short-branch](https://github.com/wangyuxiang0829/My-Perspective-on-Git/blob/master/pngs/short-branch.jpg)

* **Long-lived** such as master, develop, release

* Use `git branch` to see a list of branches in a repository

### Creating a branch

* Use `git branch <name>` to create a branch

* Creating a branch simply creates a new branch label reference but you remain still on the original branch

### Checkout

* Update the HEAD reference
* Update the working tree with the commit's files

* Use `git checkout <branch_or_commit>` to checkout a branch or commit
* Use `git checkout -b <branchname>` to combine creating and checking out a branch into a single command

### Detached HEAD

* Checking out a commit rather than a branch leads to a detached HEAD state

![](https://github.com/wangyuxiang0829/My-Perspective-on-Git/blob/master/pngs/detached-HEAD.jpg)

### Deleting a branch label

* Use `git branch -d <branchname>` to delete a branch

* If you are trying to delete a not fully merged branch, Git will not let you to do that, and if you are sure you want to delete the branch, use the command `git branch -D <branchname>` but that will lead to the dangling commits, and Git will periodically **garbage collect** looking for and deleting older dangling commits, So be careful if you use the D option
* You can use `git reflog` to return a local list of recent HEAD commits



## Merging

### Merging overview

* Merging combines the work of independent branches

![merge-commit](https://github.com/wangyuxiang0829/My-Perspective-on-Git/blob/master/pngs/merge-commit.jpg)

* Four main types of merges:
* 1. Fast-forward merge
  2. Merge commit
  3. Squash merge*
  4. Rebase*

* Fast-forward merges: Moves the base branch label the tip of the topic branch.

![fast-forward-merge](https://github.com/wangyuxiang0829/My-Perspective-on-Git/blob/master/pngs/fast-forward-merge.jpg)

* A fast forward merge is possible only if no other commits have been made to the base branch since the topic branch was created. In this example, a fast-forward merge is not possible:

![impossible-fast-forward-merge](https://github.com/wangyuxiang0829/My-Perspective-on-Git/blob/master/pngs/impossible-fast-forward-merge.jpg)

```
the basic steps to performing a fast-forward-merge:
1. git checkout master
2. git merge featureX
	* attempting a fast forward merge is the default
3. git branch -d featureX
```

### Merge commits

1.  Combines the commits at the tips of the merged branches
2. Places the result in the merge commit

```
the basic steps to performing a merge commit(if the merge is not fast forwardable):
1. git checkout master
2. git merge featureX
	* automatically attempt to create a merge commit if the merge is not fast forwardable
	* accept or modify the default merge message created by git
3. git branch -d featureX
```

```
the basic steps to performing a merge commit(if the merge is fast forwardable):
1. git checkout master
2. git merge --no-ff featureX
	* [--no-ff] means a no fast-forward merge
	* accept or modify the merge default message created by git
3. git branch -d featureX
```



## Resolving Merge Conflicts

### Merge conflict overview

* There are cases where **multiple branches make different changes to the same part of a file**, and in this case, a merge conflict occurs and a person needs to make a decision on how to resolve it
* Git can **automatically merge changes to different parts of the same file**

* In Git, a part of file is called a **hunk**, so we can say **the merge conflicts occur when two branches modify the same hunk of the same file**

### Resolving a merge conflict

1. The tip of the current branch (B) - "ours" or "mine"
2. The tip of the branch to merged (C) - "theirs"
3. A common ancestor (A) - "merge base"

![resolving-merge-conflict](https://github.com/wangyuxiang0829/My-Perspective-on-Git/blob/master/pngs/resolving-merge-conflict.jpg)

```
basic steps to resolve a merge conflict:
1. git checkout master
2. git merge featureX
	(both branches modified the same hunk in file fileA.txt in different ways)
	At this point, git will modifed fileA.txt which will show you exactly where 	the conflicts are and placed the file in your working tree.
---
at this point, if you don't want to continue to merge, you can use the command:
git merge --abort
to abort the merge
---
3. open fileA.txt and resolved the merge conflict which requires human judgement
4. git add fileA.txt
5. git commit
6. git branch -d featureX
```

* Conflicted hunks are surrounded by the marks "<<<<<<<"(ours) and ">>>>>>>"(theirs) and "=======" is between them



## Tracking Branches

### Tracking branch overview

* A tracking branch is a local branch that represents a remote branch
* A tracking branch name is like `remotename/branchname`
* **Tracking branches are only updated with network commands like clone, fetch, pull, and push**

### Viewing tracking branch names

* Use `git branch --all` to display all local and tracking branch names

* A reference named `remote/origin/HEAD` is a symbolic reference meaning that it is a reference that points to another reference, and this **specifies the default remote tracking branch**

* You can use `<remote>` name instead of the whole tracking branch name in git command

```
An example:
git branch --all
* master # checked out
  remotes/origin/HEAD -> origin/master # the default remote tracking branch
  remotes/origin/master
git  log origin/master --oneline # see the commits of our master tracking branch
git log origin --oneline # the same as before because we have default tracking branch
```

* Change the default remote tracking branch with `git remote set-head <remotename> <branch>`

### Viewing tracking branch status

* `git status` includes tracking branch status

```
git status
On branch master
Your branch is up to date with 'origin/master'. # means that as of the last time that we issued a network command like fetch, we have the latest commit in our local repository
```

* `git status` will inform you if the cached tracking branch information is out of synchronous with your local  branch

```
On branch master
Your branch is ahead of `origin/master` by 1 commit
```

