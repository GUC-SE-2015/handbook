---
layout: post
title: Introduction to Source Version Control
categories: git SVC VCS
author: nourhan
date: 2015-02-10
---
Introduction to Source Version Control
======================================
Have you ever worked with a team and got tired merging your different versions of the code? Have you ever exported several versions of your code to your local machine, just to avoid ruining it by adding new features? Have you ever wiped your code by mistake, or wondered where should you back it up? Here is the answer to all their questions and much more! Welcome to the world of source version control!
Version Control System (VCS) is a system that records changes to some certain project's files. It keeps "versions" of the code throughout the development process. The advantages of such a system may include:

  * Reverting to old versions of the code
  * Comparing the current version of the code to previous ones
  * Checking code modifications and who might have caused problems
  * Remotely backups the code
  * Code merges and conflict management



Introducing Git
===============
Git is a simple VCS that is used in maintaining versions of the code and code integration. What Git basically does is that every time you save a new version of your code, it takes a "snapshot" of the files and saves a reference to that snapshot.

The snapshots taken by Git are saved onto the local storage on a database. Users usually upload these versions to Git remote databases as a sort of backup in case of the loss of the data. Moreover, a team working on one project uploads versions of their code regularly for the sake of integration with other members of the team. We will come to how this is done later.


Terms and Definitions
=====================
Most VSCs use some common terms to denote components of the system. In this section, we will shortly introduce some of these terms and their use.


  1. Repository: is a term commonly used to denote the database of "versions" of your project. Commonly, there is a "local" repository on the machines of each of the participating developers, and a "remote" repository which is usually hosted online.

  2. Commit: is a "version" or a "snapshot" of some files within the project.

  3. Working directory: contains the local files that are changed but not yet committed.

  4. Staging area: contains a group of files that are to be committed together.
  5. Untracked files: are the files/folders that were recently added to the project but are not yet included in any commit.



Installing Git
==============

##On Windows machines
Executables are available at [here](http://git-scm.com/download/win) and [there](https://msysgit.github.io/). Installing the downloaded executables give access to a command line version of git as well as a simple GUI application.


##On Linux machines
(Ubuntu) Just fire up a terminal and run:
$ sudo apt-get install git-core
Other Linux distributions instructions can be found [here](http://git-scm.com/download/linux)

##On Mac machines
Git packages are available for download [here](http://git-scm.com/download/mac)
Or using Homebrew run the following commands on a terminal:
$ brew update
$ brew install git

Git Tree Structure
==================
Whenever a user initiates a git repository in the project root folder, git tracks all the contents of files, folders and subfolders inside this root folder. After committing the current status of the root folder - usually called the "Initial Commit" - the git tree starts with the master branch pointing at the current snapshot of the folders/files within the project. More branches can derive from the master branch. Each branch has a pointer to the current status of the project within this branch.


Gitignore
=========
Since git tracks all the files and folders from the root directory of the project, sometimes developers need to discard autogenerated files and machine-dependent configuration files from the git tree. This is to avoid conflicts and overloading the repository with unnecessary files. The .gitignore file (located in the project root directory) does the job! The .gitignore file contains a listing of the relative file paths (from the root file path) that need to be "ignored" by git. These files will no longer appear in the git working directory.
Pro Tip: never commit a file that would need to be ignored! Removing it from the commits and adding it to the .gitignore file will require more complicated operations by then!



Gitkeep
=======
Git doesn't keep track of empty folders in its tree. So to add an empty folder, an empty file named .gitkeep is added inside the folder just to allow git to be able to track it!


Getting started with Command Line Git
=====================================

1. Creating a new local repository:
  a. Change directory to the root of your source folder
   `$ cd /path/to/root/folder`
  b. initialize an empty git repository
    `$ git init`
  This creates an initial repository at the root of the source folder. All files and subfolders within this root folder can now be committed and the revisions will be kept in this git repository.

2. Committing changes:
  + Viewing the working/staging directory status:
      * `$ git status`
  lists the files staged for committing, and the files in the working directory, as well as files that are yet untracked
  + Staging Stage:
      * `$ git add <filenames-space-separated>`
  This basically adds files to the staging area, preparing them to be committed in the next step
  + Committing:
      * `$ git commit -m "commit message goes here"`
  This is the compact form for committing, which commits the files in the staging area with the commit message included between the double quotes
      * `$ git commit`
  This is the extended form for committing, which also commits the staged files. However, it opens the default terminal editor (vim, nano or others) where the committer enters a short description of the committed files, and extended description of the committed files follows in subsequent lines

3. Branching and Checkouts:
  + `$ git branch <branch_name>`
  + `$ git checkout -b <branch_name>`
  Creates a new branch with the given branch_name, and switched to this branch
  + `$ git checkout branch_name`
  Switches the working directory to the branch branch_name
  + The main and default branch is named "master" branch. The master branch usually holds the current status of the project that is fully developed and tested and proved to be fully functional.
  + Branches derive from the master branch to hold newly implemented features that are yet in the development phase or in the testing phase. Once the feature passes the test phase it is usually merged into master.
  + `$ git branch -d <branch_name>`
      Deletes the branch branch_name
  + **Note: A good branch visualizing tool is included in the references section!**


4. Adding a remote
  + `$ git remote add <remote_alias> <remote_url>`
  Defines the remote repository url under an alias name remote_alias. This is used to configure the local repository to be able to push and pull from the remote upstream. The remote_url is provided by the remote repository host such as Github, Bitbucket or Gitlab.


5. Cloning an existing repo
  + `$ git clone <remote_url>`
  Clones the remote repository located at remote_url into the current directory.

6. Uploading and Downloading
  + Pushing to upstream (Uploading code)
      + `$ git push <remote_alias> <branch_name>`
      Pushes (or uploads) the unsynced commits from the local repository from the current `branch_name` to its remote equivalent on the remote denoted by 
      `remote_alias`.  The most commonly default `remote_alias` is "origin".
      + `$ git push <remote_alias> <src_branch_name>:<dst_branch_name>`
      Pushes the unsynced commits from the source local branch `src_branch_name` to the remote branch `dst_branch_name` on the remote `remote_alias`.
  + Pulling from upsteam (Downloading code)
      + `$ git pull <remote_alias> <branch_name>`
      Pulls (or downloads) commits from the remote branch `branch_name` that are not existing on the local branch `branch_name` and merges them automatically, from the remote `remote_alias`.
  + **Note: Always pull the upstream before pushing so that you would be able to resolve conflicts first!**

7. Merging and conflicts
  + Merging
      + `$ git merge <branch_name>`
      Merges the branch branch_name into the current branch
      **Note: The pull git option auto merges the pulled branch into the current one.**
  + Conflict Resolution

    ```
      <<<<<<<<<<<<<<<<<<<< old branch
      .... old code goes here
      ====================
      .... new code goes here
      >>>>>>>>>>>>>>>>>>>> new branch
    ```
    This is an example of a conflict. This structure is present in any file having conflicts. The proper way to resolve conflicts is to `$ git status` in order to know which files have conflicts. Navigate to each of these files searching for the above structure. Once found, the developer is required to compare the two versions of the code (the old and new code versions detected by git) and either keep both or delete both. The lines containing `>>>`, `<<<` and `===`should also be eliminated.
8. Log and Diffs:
  + `$ git log`
  Prints a log with the commits on current branch, listed most-recent-first.
  + `$ git diff`
  Show differences between your current working directory and the staged files for committing.
  + `$ git diff --cached`
  Show differences between the staged files for committing and the most recent commit.
  + `$ git diff HEAD`
  Show the differences between your working directory and the most recent commit.
  + `$ git diff <commit_id> <commit2_id>`
  Shows the differences between the commit with id `commit_id` and the commit with id `commit2_id`. Commit IDs are found in the log displayed by the `$ git log` command
  The `diff` command prints the file differences with added lines coloured in green and starting with a `+`, and the deleted lines coloured in red and starting with a `-`.
9. Stashing
  + `$ git stash`
  Switching between branches require the working directory to be clean - everything has to be committed. Sometimes we want to save the current status without committing it, until we return to the current branch. Stashing pushes the current status of the un.committed files to a stack for retrieval and cleans the working directory to the last committed state.
  + `$ git stash apply`
  Pops the most recently stashed status.
10. Additional commands
    + Local git Username Configuration
      + `$ git config --global user.name "John Doe"`
      Sets the username for git that would be attached to the commits and viewable in the remote, to the denoted name between the double quotes (here John Doe)
    + Local git Email Configuration
      + `$ git config --global user.email johndoe@example.com`
      Sets the email for git that would be attached to the commits and linked to the remote user, to the denoted email after user.email (here johndoe@example.com)
    + Local git Proxy Setting (for on campus push and pull using GUC-WiFi)
      + `$ git config --global http.proxy http://username:password@50.0.0.5:8080`
      Sets the git proxy to the GUC proxy settings using the GUC username and password. 
      **Note: Please don't include @ or ! signs in your GUC passwords!**
    + Local git Proxy Unsetting (for off campus push and pull)
      + `$ git config --global --unset http.proxy`
      Unsets the proxy settings.


Good Practices
==============

1. Modular commits
  + Always commit relevant files together. Never commit all files together.
2. Descriptive commits
  + The description of the commit should reveal the files changed and highlights the most important changes. This is for developers to be able to quickly pinpoint what was the status of the files included in the commit without having to check the actual code.
3. Regular commits
  + Regularly commit your work even if it is yet unfinished. This helps track the status of the work and saves the work done so far
4. Regular push
  + Regularly push your work to the relevant remote branch after committing! Pushing backs up your work on the upstream so that any physical damage to the machine or any deletion to the files would be recoverable since the work is already online!


References
==========
[Gitbook](http://git-scm.com/book/en/v2/Getting-Started-About-Version-Control)

[Git Cheatsheet](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf)

[Learn Git Branching](http://pcottle.github.io/learnGitBranching/)

[Live Tutorial](https://try.github.io/levels/1/challenges/1)