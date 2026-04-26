# Git Cheat Sheet

## Basic grammer

### Getting started

start a new repo 
```bash
 git init 
 ```

clone an existing repo 
```bash
 git clone repo
 ```

 ### prepare to commit

 add untracked file or unstaged changes

 ```bash
 git add <file>
 ```

 Choose what parts of a file to stage:

  ``` bash
 git add -p
 ```

 Add all  unstaged files or unstaged changes

 ```bash
 git add .
 ```

 check what you added
 ``` bash
 git status
 ```

 unstage one file:

 ``` bash
 git reset <file>
 ```

 unstage everything:

  ``` bash
 git reset
 ```

### modify files

Delete file:

 ``` bash
 git rm <file>
 ```

 Telling git to forget about a file without deleting it

  ``` bash
 git rm --cached <file>
 ```

 Move file:

  ``` bash
 git mv <old> <new>
 ```

 ### make commits

 Make a commit

  ``` bash
 git commit -m 'message'
 ```

 commit all unstaged changes:

  ``` bash
 git commit -am 'message'
 ```

 ### Move between branches

 switch branches:
  ``` bash
 git switch <name>
 ```
 or
  ``` bash
 git checkout <name>
 ```

 create branches
  ``` bash
 git switch -c <name>
 ```
 or
  ``` bash
 git checkour -b <name>
 ```

 list branches
  ``` bash
 git branch
 ```
 list of branches by mostly revently committed to: 
  ``` bash
 git branch --sort=-committerdate
 ```
 Delete a branch
  ``` bash
 git branch -d <name>
 ```
force delete a branch
 ``` bash
 git branch -D <name>
 ```

 ### Diff staged/unstaged changes

 diff all staged and unstaged changes:
  ``` bash
 git diff HEAD
 ```

 Diff just staged changes:
  ``` bash
 git diff --staged
 ```

 diff just unstaged changes
  ``` bash
 git diff
 ```

 ### Diff Commits

 show diff between a commit and its parent
  ``` bash
 git show <commit>
 ```

 Diff one file since a commit:
  ``` bash
 git diff <commit> <file>
 ```
  Diff two commits
   ``` bash
 git < commit> <commit>
 ```
 show a summary of a diff
  ``` bash
 git diff <commit> --stat
 ```
 or
  ``` bash
 git show <commit> --stat
 ```

 Discard your changes
 

