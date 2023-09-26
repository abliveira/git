# Git Commands

## Table of contents

1. [Help commands](#help-commands)</br>
    1.1. [git](#git)</br>
    1.2. [git help](#git-help)</br>
2. [Files](#files)</br>
    2.1. [git add](#git-add)</br>
    2.2. [git rm](#git-rm)</br>
    2.3. [git mv](#git-mv)</br>
    2.4. [git ls-files](#git-ls-files)</br>
3. [Commits](#commits)</br>
    3.1. [git commit](#git-commit)</br>
    3.2. [git diff](#git-diff)</br>
    3.3. [git status](#git-status)</br>
    3.4. [git log](#git-log)</br>
    3.5. [git revert](#git-revert)</br>
    3.6. [git reset](#git-reset)</br>
    3.7. [git blame](#git-blame)</br>
    3.8. [git bisect](#git-bisect)</br>
4. [Branches](#branches)</br>
    4.1. [git branch](#git-branch)</br>
    4.2. [git checkout](#git-checkout)</br>
    4.3. [git merge](#git-merge)</br>
    4.4. [git rebase](#git-rebase)</br>
5. [Repositories](#repositories)</br>
    5.1. [git clone](#git-clone)</br>
    5.2. [git fetch](#git-fetch)</br>
    5.3. [git pull](#git-pull)</br>
    5.4. [git push](#git-push)</br>
    5.5. [git show](#git-show)</br>
    5.6. [git gc](#git-gc)</br>
    5.7. [git fsck](#git-fsck)</br>
    5.8. [git prune](#git-prune)</br>
    5.9. [git daemon](#git-daemon)</br>

## Help commands 

### git

Get a basic list of git commands

```bash
git
```

Get the git version installed

```bash
git --version
```

### git help

Get a basic list of git commands

```bash
git help
```

Get a more complete set of commands

```bash
git help --all
```

Get help on a particular command

```bash
git help commit
```

Or

```bash
man git-commit
```

## Files

### git add

Adds new or changed files in your working directory to the Git staging area

Stage a specific directory or file

```bash
git add <path>
```

### git rm

Removes a file from the working tree and the index

you want to remove a file that has been staged but not committed, you have to add the -cache option, as in:

```bash
$ git add myfile
$ git rm myfile --cached
```

### git mv

Renames a file and stages the new filename in the repository. The binary blobs associated with the file remain the same, only the index is updated

### git ls-files

Shows information about files in the index and working tree. By default, this command shows only files in the repository

## Commits

### git commit

Shortcut command that immediately creates a commit with a passed commit message

```bash
git commit -m "commit message"
```

Only commit changes from one file

```bash
git commit -s file1
```

If you want to commit all changes,, any of these forms will do it:

```bash
$ git commit -s
$ git commit ./ -s
$ git commit -a -s
```

Every time you do a commit, git assigns a unique 160-bit 40-character hexadecimal hash value to it

### git diff

Display differences in a number of ways

Shows the differences between the current version and the last commit

```bash
git diff
```

Shows the differences between the current version and a given commit

```bash
git diff earlier_commit
```

Shows the differences between the staged changes in the index and a given commit

```bash
git diff --cached earlier_commit
```

Shows the differences between two commits

```bash
git diff one_commit another_commit
```

It is possible to get only brief statistics using --stat

```bash
git diff --stat one_commit another_commit
```

It is possible to refine the search path

```bash
git diff --stat one_commit another_commit directory1/directory2
```

### git status

Displays the state of the working directory and the staging area

```bash
git status
```

### git log

Display the history of commits

```bash
git log
```

Display a brief history of commits

```bash
git log --oneline
```

### git revert

You can back out a particular commit with

```bash
git revert commit_name
```

commit_name can be specified in a number of ways and need not be the most recent

Commits can be delineated with:

HEAD : most recent commit

HEAD~ : previous commit (the parent of HEAD)

HEAD~~ or

HEAD~2 : the grandparent commit of HEAD

{hash number} : specific commit by full or partial sha1 hash number

{tag name} : a name for a commit.

Note that git revert puts in a new commit set of changes, i.e. a reversed patch as an additional commit. This is the appropriate thing to do if someone else has downloaded a tree containing the changes that have been reversed. This will change your working copy of source files.

In short, git revert builds and adds a new commit object, sets HEAD to it and updates the working directory (changes induced by git revert):

Uncommitted changes discarded

New commit created; no actual commits removed

### git reset

Discard uncommitted changes

--soft: just moves the current branch to prior commit object (index unchanged in this case)

--mixed (default): also updates the index to match new head (un-stages everything)

--hard: same as --mixed, but also updates working directory to match new head (un-edits your files)

### git blame

shows the commutis of a file and the author responsible

```bash
git blame file
```

### git bisect

Use binary search to find the commit that introduced a bug. bisect helps to test commits until you find a good one. if a bad change has been done somewhere in the last 1024 commits, you can find it in no more than 10 bisection steps

```bash
git bisect <subcommand> <options>
```

Type:

```bash
$ git bisect start
$ git bisect bad                 # Current version is bad
$ git bisect good v2.6.13-rc2    # v2.6.13-rc2 is known to be good
```

git now will iterate using binary search. If the version commit is bad, type:

```bash
git bisect bad
```

if the commit loaded is good, type

```bash
git bisect good
```

to clean up the bisection state and return to the original HEAD:

```bash
git bisect reset
```
When done, check the history of your bisection with

```bash
git bisect logs
```

## Branches

### git branch

List the branches

```bash
git branch
```

List the branches with a detailed history

```bash
git branch -v
```

Creating a new branch

```bash
git branch [branch_name] [starting_point]
```

If you no starting_point provided, a copy of the active branch as of its last commit will be created

```bash
git branch [branch_name]
```

Delete a branch. It cannot be the current branch

```bash
git branch -d [branch_name]
```

### git checkout

Switch from the current working branch to another

```bash
git checkout [target_branch_name]
```

Note: Git will refuse to change if there's uncommited files in the current working branch

### git merge

Before merging, checkout to the target branch, such main. Is recommended to commit or remove any pending changes to avoid confusion later

```bash
git merge [target_branch_name]
```

### git rebase

If a branch was created from another, such the main branch, and the main branch had newer commits, it is possible to apply the commits from the main to the splited branch, pushing foward the commits of the splited branch. In summary, the splitted branch incorporate the latest changes from another branch, without yet merging this branch into the other branch

```bash
$ git checkout develop
$ git rebase main develop
```

Before
    
            A---B---C develop
            /
    D---E---F---G master

After rebase

                    A'--B'--C' develop
                    /
    D---E---F---G master

Some conflicts may be solved in order to complete the rebase

## Repositories

### git clone

Cloning a repository to a specific folder

```bash
git clone <repo_address>
```

Cloning to a specific folder

```bash
git clone <repo_address> <directory>
```

### git fetch

Downloads contents from a remote repository

```bash
git fetch
```

### git pull

Update the local repository with changes made at the remote site. Basilcally, it's the `git fetch` and `git merge` commands used together

```bash
git pull <options>
```

### git push

Update the remote repository with changes made at the remote local

```bash
git push <repo_address>
```

### git show

Show details about a particular item, such a file or commit

```bash
git show <options> <object>
```

Show details about the local repository

```bash
git show-ref
```

Show details about the remote repository

```bash
git ls-remote <repo_address>
```

Example: Shows a file from a particular commit

```bash
git show 650bb48:main.c
```

To exit, type 'q'

### git gc

Optimize and compact the repository

```bash
git gc
```

### git fsck

Check your repository for certain kinds of errors with the command. The most likely and harmless errors it will find will be dangling objects

```bash
git fsck
```

### git prune

Deletes all the files that are not reachable from the current branch

```bash
git prune
```

-n
--dry-run
Do not remove anything; just report what it would remove

### git daemon

A really simple server for Git repositories

```bash
git daemon <options>
```