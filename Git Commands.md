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

$ git add myfile
$ git rm myfile --cached

### git mv

Renames a file and stages the new filename in the repository. The binary blobs associated with the file remain the same, only the index is updated

### git ls-files

Shows information about files in the index and working tree. By default, this command shows only files in the repository

## Commits

### git commit

only want to commit the changes to one file

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

### git log

display the history of commits with git using the command git log

### git revert

You can back out a particular commit with

```bash
git revert commit_name
```

commit_name can be specified in a number of ways and need not be the most recent.

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

git bisect <subcommand> <options>

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

## Managing Repositories

### git gc

Optimize and compact the repository

```bash
git gc
```

### git fsck

check your repository for certain kinds of errors with the command. The most likely and harmless errors it will find will be dangling objects

```bash
git fsck
```

### git prune

deletes all the files that are not reachable from the current branch

```bash
git prune
```

-n
--dry-run
Do not remove anything; just report what it would remove.