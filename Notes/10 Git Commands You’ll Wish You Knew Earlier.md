---
tags:
- github
---
## **10 Git Commands You’ll Wish You Knew Earlier

Git can feel intimidating when you’re starting out. Most of us stick to the basics: `git add`, `git commit`, and `git push`, and honestly, that works… until it doesn’t. At some point, you’re going to hit a roadblock—a tangled history, a broken branch, or a bug you just can’t trace.

That’s when these 10 Git commands become lifesavers.

**1\. git reflog**
Ever made a mistake so bad you wished you could turn back time? **git reflog** is the time machine you didn’t know you had.

What it does:

It tracks every single thing you’ve done in your repository—even commits you thought were lost.

When to use:

-   You accidentally deleted a branch.
-   You need to recover a commit after a bad reset.

Command:

`git reflog`

**2\. git cherry-pick**
Imagine this: there’s one perfect commit on another branch, and you need it now without merging the entire branch. That’s where `git cherry-pick` comes in.

What it does:

It lets you pick specific commits from one branch and apply them to another.

When to use:

-   You want a bug fix from `feature-branch` in `main` without merging the entire branch.

Command:

`git cherry-pick <commit-hash>`

**3\. git bisect**
Debugging a bug that suddenly appeared? Instead of manually checking each commit, let Git do the detective work for you.

What it does:

Performs a binary search through your commit history to find the exact commit that introduced a bug.

When to use:

-   When you have a bug, but you’re not sure which commit caused it.

Command:

`git bisect start   git bisect bad # Mark the current commit as bad   git bisect good <commit-hash> # Mark a known good commit`

Git will keep narrowing down the commits until it finds the culprit.

**4\. git stash pop**
You’ve been there—halfway through coding when a critical bug report comes in. You need to switch branches without losing your work.

What it does:

-   Stashes your uncommitted changes so you can come back to them later.

Why pop?

`git stash` saves your work, but `git stash pop` restores it and removes it from the stash list, keeping things tidy.

Command:

`git stash pop`

**5\. git reset --soft**
Ever made a commit and realized you weren’t ready yet? Maybe you forgot to squash it with the previous one?

What it does:

Moves your commit back to the staging area without losing your changes.

When to use:

-   You want to rework a commit without losing progress.

Command:

`git reset --soft HEAD~1`

**6\. git blame**
Yes, the name sounds accusatory, but it’s not about pointing fingers (or maybe it is).

What it does:

Shows who last modified each line in a file.

When to use:

-   You’re trying to understand why a particular change was made.

Command:

`git blame <file>`

**7\. git log --oneline --graph**
Looking at a repository with multiple branches can feel overwhelming. This command gives you a bird’s-eye view of your project.

What it does:

Displays your commit history in a simple, visual format.

When to use:

-   To understand the history of a branch or how branches diverged and merged.

Command:

`git log --oneline --graph --all`

**8\. git clean -f**
Sometimes, your working directory gets messy—untracked files piling up everywhere. `git clean` is like a spring cleaning for your repo.

What it does:

Removes untracked files from your working directory.

When to use:

-   You’ve tried to git pull, but it’s failing due to conflicting untracked files.

Command:

`git clean -f`

**9\. git rebase -i**
Interactive rebasing is the magic wand for cleaning up messy commit histories.

What it does:

Lets you squash, edit, or delete commits during a rebase.

When to use:

-   Before merging, to make your commit history look clean and professional.

Command:

`git rebase -i HEAD~<number-of-commits>`

Pro tip: Use this sparingly on public branches to avoid conflicts.

**10\. git diff --staged**
Before committing, wouldn’t it be nice to see exactly what’s staged? That’s where git diff --staged comes in.

What it does:

Shows changes between your staging area and your last commit.

When to use:

-   Double-checking staged changes before committing.

Command:

`git diff --staged`

Which of these commands are new to you? Or do you have an underrated favorite that didn’t make the list? Let’s hear it in the comments!

[[Git]]  [[GitHub]]