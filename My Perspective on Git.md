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

