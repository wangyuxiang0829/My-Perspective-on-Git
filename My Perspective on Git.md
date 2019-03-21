# My Perspective on Git

## Git Overview

### What is a git repository?

* A series of **snapshots** or **commits**.

## Locations of Git

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

* If have a local repository, you want to **push** to a remote repository, than you will **add** the remote repository to your local repository.
* If not have a local repository, you will **clone** the remote repository which will create a local repository that is associated with the remote repository.

### Clone a remote repository

* A clone is a local copy of a remote repository.

* A reference to the remote repository is included in the local repository. So you can synchronize the repository.
* **origin** is the default alias for the remote repository URL.
* `git clone <url/to/projectname.git> [localprojectname]` is used to create a local copy of a remote repository. The last argument is optional. Cloning will create a project directory in your local computer.
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
  * `-u` track this branch (--set-upstream)
  * The arguments after `git push` are all optional, because git will assume default information or use previous arguments after you have executed the first push.
* A successful push synchronizes the branches on the local and remote repositories so that they they contain exactly the same commits.
* Before you run `git push` command you can use `git remote --verbose` command to ensure that your local repository has an association with the remote repository.