# Git Cleanup Merged

This is a simple git extension for cleaning up all the already merged into master development branches.

## What does it do?

So, you've created a dev branch, pushed it to the remote origin and it was accepted and then merged into the master branch. The branch was deleted from the remote origin since no further work is needed.

Now, your local repository is left with a branch that was merged into master and is probably no longer needed. This is not a problem, just `git branch -d` and it is gone! But what happens when you are working with multiple branches? You'll have to keep track of them all. Manually check whether they've been merged and then find the few which you should delete form your local copy. Or you just want to save yourself a few seconds from typing the whole branch deletion command.

## Usage

So, we have ourselves in this branching situation:

```sh
$ git branch -l
  2015
* master
  quiz02
  task-01
```

There are a few. Some may be already merged, others - not. But first, lets just make sure we have latest changes as good gitland citizens.

```
$ git pull --prune
From github.com:org/progject
 x [deleted]         (none)     -> origin/quiz02
...
```
A-ha! `quiz2` was deleted. Gotcha! See, everything I needed is in the `git pull` output? Anyway, lets run the script:

```
$ git cleanup-merged
Deleted branch 2015 (was b7ea0d1).
Deleted branch quiz02 (was 73f21c9).
Deleted branch task-01 (was 4c209cf).
```

Oh wow! It seems that the other two have been merged as well. Just you haven't noticed before. See? Removed clutter you probably did know about.

## Installation

Place the `git-cleanup-merged` script in your `$PATH`. Personally, I am using `~/bin` for this. Make sure it has exec permissions.

## Cаveats

The master branch would never be deleted. The currently selected branch would never be deleted as well.
Only information in the local branch is used. So regular `git pull --prune` is your friend.

## Shorter alias in gitconfig

Writing 'cleanup-merged' is unnecessary long. For my taste even the bash completion does not help. So this little alias in `~/.gitconfig` does wonders:

```
[alias]
    cm = cleanup-merged
```

Then you can use it by just typing

```
$ git cm
```
