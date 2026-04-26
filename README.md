# Git Cheat Sheet

Git is a system that lets developers create, manage, compare, share, and restore project snapshots across multiple timelines

## Structure
.git/
│── HEAD           --> current position pointer
│── config         --> stores project settings
│── objects/       --> git data as compressed objects ( objects are hashed)
│── refs/          --> named pointers
│── logs/          --> tracks reference movement ( used in recovery)
│── index          --> staging area


**objects/** 
Git mainly stores:

- blobs --> file contents
- trees --> file structure
- commits --> snapshots + metadata
- tags

A commit stores:
- pointer to tree
- author
- timestamp
- message
- parent commit

Stores project settings:
- remote URLs
- branch tracking
- merge settings

**Git is action based** :
(think in verbs)

| Verb    | Meaning               |
| ------- | --------------------- |
| add     | prepare changes       |
| commit  | save snapshot         |
| push    | send to remote        |
| pull    | receive updates       |
| fetch   | download updates only |
| clone   | copy repo             |
| branch  | manage branches       |
| merge   | combine histories     |
| switch  | change branch         |
| restore | undo file changes     |
| reset   | move history pointer  |
| status  | inspect state         |
| log     | view history          |

**workflow mastery**

We’ll cover:
- Starting projects
- Team collaboration
- Pulling updates safely
- Fixing conflicts
- Feature branches
- Clean commit habits
- Production deployment flow


**Debugging & recovery**

Learn how to recover from:
- Wrong commits
- Deleted files
- Merge conflicts
- Detached HEAD
- Broken branches
- Accidentally pushed secrets
- Undo mistakes safely

## Roadmap

**Phase 1** — Understand Git Core
- What is Git?
- Why developers use it
- Git architecture
- Local workflow
**Phase 2** — Command Fluency
- init
- clone
- add
- commit
- status
- log
**Phase 3** — Collaboration
- branch
- checkout / switch
- merge
- pull
- push
- fetch
**Phase 4** — Advanced
- rebase
- stash
- cherry-pick
- reset
- reflog
**Phase 5** — Real World
- GitHub workflows
- Open source contribution
- CI/CD

## Basic grammer

```bash
git <verb> <target> <options>
```

long flag -- 
short flag - 
## basic workflow map

Start Work
↓
Get Latest Code
↓
Create / Switch Branch
↓
Code Changes
↓
Stage Changes
↓
Commit Changes
↓
Push to Remote
↓
Open Pull Request / Merge
↓
Repeat



## Resources

[git cheat sheet](https://git-scm.com/cheat-sheet)

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

### Discard your changes

Delete unstaged changes
  ``` bash
 git restore <file>
 ```
or
  ``` bash
 git checkour <file>
 ```

Delete all staged and unstaged changes to one file
  ``` bash
 git restore --staged --worktree <file>
 ```
 or
   ``` bash
 git checkout HEAD <file>
 ```
 Delete all staged and unstaged changes:
   ``` bash
 git reset --hard
 ```
Delete untracked files
  ``` bash
 git clean
 ```

 'Stash' all staged and unstaged changes:
   ``` bash
 git stash
 ```

### Edit history

"Undo" the most recent commit ( keep your working directory the same)
  ``` bash
 git reset HEAD^
 ```

squash the last 5 commits into one:
  ``` bash
 git rebase -i HEAD~6
 ```
 undo a failed rebase
   ``` bash
 git reflog BRANCHNAME
 git reset --hard <commit>
 ```

 Change commit message (or add a file you forgot)
   ``` bash
 git commit --amend
 ```

 ### Code archaeology

 Look at branch's history:
   ``` bash
 git log main
 git log --graph main
 git log  --online
 ```

 show every commit that modified a file
   ``` bash
 git log <file>
 ```
 
 show every commit that modified a file, including before it was renamed
   ``` bash
 git log --follow <file>
 ```

 Show who last changed each line of a file
   ``` bash
 git blame <file>
 ```
 Find every commit that added or removed some text
   ``` bash
 git log -G banana
 ```

 ### Combined Diverged Branches

Combine with rebase
  ``` bash
 git switch banana
 git rebase main
 ```
 combine with merge
   ``` bash
 git switch main
 git merge <another branch>
 ```
combine with squash merge
  ``` bash
 git switch main
 git merge --squash <another branch>
 git commit
 ```

Bring a branch up to date with another branch
  ``` bash
 git switch main
 git merge < another branch>
 ```
copy one commit onto the current branch:
  ``` bash
 git cherry-pick <commit>
 ```
 ### Restore an old file

 Get the version of a file from another commit
   ``` bash
 git checkout <commit> <file>
 ```
 or
   ``` bash
 git restore <file> --source <commit>
 ```

 ### Add a Remote
   ``` bash
 git remote add <name> <url>
 ```

 ### Push Your Changes

 Push the `main` branch to the remote `origin`:
   ``` bash
 git push origin main
 ``` 
 Push a branch that you've never pushed before:
   ``` bash
 git push -u origin <name>
 ```
 push tags:
   ``` bash
 git push --tags
 ```

 Push the current branch to its remote "tracking branch"
   ``` bash
 git push
 ```
 Force push:
   ``` bash
 git push --force-with-lease
 ```

 ### pull changes
  fetch your chanegs ( but don't change any of your local branches):
``` bash
 git fetch origin main
 ```

 Fetch changes and then rebase your current branch:
   ``` bash
 git pull --rebase
 ```

 Fetch changes and then merge them into your current branch:
   ``` bash
 git pull origin main
 ```
 or
   ``` bash
 git pull
 ```

 ### Configure Git

 set a config option:
   ``` bash
 git config user.name ' your name '
 ```

 Set option globally:
   ``` bash
 git config --global...
 ```

 Add an alias:
   ``` bash
 git config alias.st status
 ```

 See all possible config options
   ``` bash
 man git-config
 ```

 ### Important files

 Local git config
   ``` bash
 .git/config
 ```
 Global git config:
   ``` bash
 ~/.gitconfig
 ```

 List of files to ignore:
   ``` bash
 .gitignore
 ```