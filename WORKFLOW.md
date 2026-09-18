# Git Team Sync Workflow

## 1. Why was the push rejected?

The push from Clone B was rejected because the remote `feature/loyalty-points` branch contained commits that Clone B did not have locally. Git reported:

`[rejected] ... (fetch first)`

and:

`remote contains work that you do not have locally`

This happened because Clone A had already pushed a change to the same branch. Clone B then tried to push its own different history without first integrating the remote changes.

The second rejected push happened for the same reason: Clone B had already pushed a merge commit, while Clone A made another local commit before fetching the updated remote branch.

## 2. Merge vs. rebase

In Task 3, I used `git merge` to combine the changes from Clone A and Clone B. This created a merge commit and preserved both branches' histories.

In Task 4, I used `git rebase` instead. The local Task 4 commit was replayed on top of the updated remote branch. This created a new commit with a new commit ID and produced a conflict that had to be resolved before the rebase could continue.

## 3. One habit that can avoid both rejected pushes

Before pushing changes to a shared branch, fetch the latest remote changes and make sure the local branch is up to date. This reduces the chance of pushing from an outdated branch.

## 4. Merge or rebase on a shared team branch?

For a shared team branch, merge can be useful because it preserves the history of how separate branches were combined. Rebase can make history more linear, but it rewrites commit history, so it should be used carefully on branches that other team members are already using.