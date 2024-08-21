# 1 Git Basics

This chapter covers all the basic local Git oprations:
* creating or cloning a reponsitory;
* staging and committing those changes;
* remote repository;
* viewing the history of all the changes the repository.

## 1.1 Cloning an Existing Respository
```
$ git clone <url>
```
when you run `git clone`, every version of every file for the history of the project is pulled down by default.

### 1.1.1 For Example

```
$ git clone https://github.com/huabin91/test/demo1
```
Details of the progress after this step of operation:
1.  **create** a directory named demo1;
2. **initializes** a `.git` directory inside it;
3. **pulls down** all the data for that repository;
4. **checke out** a working copy of **the lastest version**.  

## 1.2 Access Git Repository

Git can use major protocols to transfer data: Local, HTTP, **Secure Shell (SSH)**。

### 1.2.1 The SSH Protocol
SSH access to server is already set up in most places. To clone a Git repository over SSH:

```
$ git clone ssh://user@servier:project.git
or
$ git clone user@servier:project.git
```
But before using the SSH protocol to access the Git server, we need to add our **personal SSH public key** to the Git server.

you schould check to mack sure you don't already have a key. By default, a user's SSH keys are stored in that user's `~/.ssh` directory.

```
$ cd ~/.ssh
$ ls
	id_dsa
	id_dsa.pub
```
If you don't have these files, you can create them by running a progam called `ssh-keygen` (specific operation please check online). 
 All they have to do is copy the contents of the `.pub` file add to Git server.

## 1.3 Recording Changes to the Repository
You need to mack some changes and commit snapshots of those changes into your repository.

<img src="https://github.com/huabin91/mein-profil/blob/main/1-Programmierkenntnisse/4-Ressource/git-base-record-lifecycle-file.png?raw=true">

**Remember** that each file in your working directory can be in one of two states: `tracked` or `untracked`. Tracked files are files that were in the last **snapshot**. they can be `unmodified`, `modified`, or `staged`. Untracked files are everything else (any files in your working directory that were not in you last snapshot and not in your staging area).

**Untracked** basically means that Git sees a file you don't have in the previous snapshot (commit).

### 1.3.1 Checking the Status of Your Files
```
$ git status
```
### 1.3.2 Tracking News Files
```
$ git add <file> / git add .
```
Add this content to the next commit. **If you modify a file after you run git add, you have to run git again to stage the lastest version of the file.**
### 1.3.3 Committing Your Changes
```
$ git commit -m "<commit message>"
```
## 1.4 View the Commit History
```
$ git log 
```
### 1.4.1 Output-Formatting Options
* `git log -p`, show the difference introduced in each commit;
* `git log --stat`,  prints a list of modified files, how many files were changed, and how many lines in those files were added and removed;
* `git log --pretty=?`, a few prebuild options: oneline, short, full, fuller, format. 
### 1.4.2 Limiting Options
Options that let you show  only a subset of commits.

## 1.5 Undoing Things
### 1.5.1 after commit, also add new files / modify commit message
When you commit too early and possibly forget to add some files, or you muss up you commit message.
```
$ git commit --amend
$ git commit -m '<commit new message>'
$ git add <forgotten_file>
$ git commit --amend
```
### 1.5.2 Unstaging a Staged File
```
$ git reset HEAD <file>
```
The file is modified but once again unstaged. If you call it with `--hard`, in this instance the file in your working directory is tocued.
### 1.5.3 Unmodifying a Modified File
```
$ git checkout -- <file> 
```
If you realize that you don't want to keep your changes to the file, easily unmodify it - revert to what it looked like when you last committed.

## 1.6 Removing Files
To remove a file from Git, you have to **remove it from your tracked files and then commit**; 
If you modify the file and added it to the index already, you must force the removal with the -f option.
```
$ git rm <file> 

$ git rm --cached <file>
```
## 1.7 Working with Remotes

 ### 1.7.1 Showing Your Remotes
```
$ git remote -v
```
### 1.7.2 Adding Remote Repositories
```
$ git remote add <shortname> <url>
```
### 1.7.3 Fetching and Pulling from Your Remotes
```
$ git fetch <remote-name>
```
The `git fetch` command pulls the data to your local repository, it doesn't automatically merge it with any of your work or modify what you're currently working on. You have to merge it manually into your work when you're ready.
```
$ git pull <remote-name>
```
You can use the `git pull` command to automatically fetch and then merge a remote branch into your current branch.
### 1.7.4 Pushing to Your Remotes
```
$ git push <remote-name> <branch-name>
```
## 1.8 Ignoring Files

you can create a file listing patterns to match them named `.gitignore`. Setting up a `.gitignore` file before you get going is generally a good idea so you don't accidentally commit files that you really don't want in your Git repository

```
*.a         # no .a files
!.a         # but to track lib.a, event though you're ignoring .a files above
/TODO       # only ignore the root TODO file, not subdir/TODO
build/      # ignore all files in the build/ directory
doc/*.txt   # ignore doc/notes.txt, but not doc/server/arch.txt
```

Github maintains a fairly comprehensive list of good .gitignore file examples for dozens or projects and languages at https://github.com/github/gitignore .

# 2. Git Branching
## 2.1 Branch Management
If you run it with no arguments, you get a simple listing of your current branches:
```
$ git branch
	iss53
*	master
	testing
```
Notice the `*` charracter that prefixes the master branch: it indicates the branch that you currently have checked out (the Branch that HEAD points to). This means that you commit at this point, the master branch will be moved forward with your new work.
### 2.1.1 Creating a New Branch
**Create a branch for a new story you're working on.**

You want to create a new branch called testing, you do this with the `git branch` command:
```
$ git branch testing
```
### 2.1.2 Switching Branches
To switch to an existing branch, you run the `git checkout` command:
```
$ git checkout testing
```
It's important to note that when you switch branches in Git, files in your working directory will change. If you switch to an older branch, your working directory will be reverted to look like it did the last time you committed on that branch. If Git cannnot do it cleanly, it will not let you switch at all.

Before you do that, note that if your working directory or staging area has uncommitted changes that confict with the branch you're checking out, Git won't let you switch branches. It's best to have a  clean working state when you switch branches. 

To create a branch and switch to it at the same time, you can run the `git checkout` command with the `-b` swicth:
```
$ git checkout -b iss53
=
$ git branch iss53
$ git checkout iss53
```
Switched to a new branch iss53.
### 2.1.3 Basic Merging
All you have to do is check out the branch you want to merge into and then run `git merge` command:
```
$ git checkout master
$ git merge iss53
```
### 2.1.4 Basic Merge Conflicts
Git hasn't automatically created a new merge commit. It has paused the process while you resolve the conflict. If you want to see which files unmerged at any point after a merge conflict, you can run `git status`.
