Tags: #git #utilities 

Rebasing seems scary until you realize you can roll back most everything.  A rebase that "evaporates" one or more commits can be undone by identifying the commits in question from the reflog and reintegrating them wherever necessary.

The `reflog` records every position of `HEAD` for the last 30 days.  This allows review of individual commits via `git reflog`  so they can be recovered.

The following shows an interactive rebase attempting to operate on all revisions (`git rebase -i 54effd9 --root`) which inadvertently dropped everything but the initial commit (`54effd9`).  Post rebase the new contents of the `main` branch were _only_ `b00c593` which looked like all unpushed changes were lost, though `git reflog`  shows the previous history that allows recovery from the faulty rebase.

```shell
$ git reflog
b00c593 (HEAD, main) HEAD@{0}: reset: moving to b00c593
1e30806 HEAD@{1}: rebase -i (pick): Topic: Knowledge Graph Initial Addition
1ae517c HEAD@{2}: rebase -i (pick): Topic: Knowledge Graph Initial Addition
1c68fcb HEAD@{3}: rebase -i (start): checkout 1c68fcb9d979e860c66db408fb9caf140ac7a78c
54effd9 HEAD@{4}: rebase -i (start): checkout 54effd9
b00c593 (HEAD, main) HEAD@{5}: commit: Topic: Knowledge Graph Snapshot Update
e403347 HEAD@{6}: commit: Topic: Knowledge Graph Machine Learning Dataset Formatting Update
3dbff58 HEAD@{7}: commit: Topic: [REBASE] Remove these
2da3f87 (origin/main) HEAD@{8}: commit: Topic: Knowledge Graph Snapshot Update
025e023 HEAD@{9}: commit: Topic: Creative Commons Attribution Share Alike 4.0 License Addition
fb0a9e9 HEAD@{10}: commit: Topic: Knowledge Graph Snapshot Update
54effd9 HEAD@{11}: reset: moving to HEAD~
c26577d HEAD@{12}: commit: Topic: Knowledge Graph Snapshot Update
54effd9 HEAD@{13}: Branch: renamed refs/heads/master to refs/heads/main
```

For reference, recovering from the above was done by:
1. Checkout the old `HEAD` with `git checkout 54effd9`. This detaches from any branch.
2. Rebase correctly. 
3. Delete the previous branch, so the newly rebased history can be put in its place with `get branch -D main`
4. Create a new branch using the old name with `get checkout -b main` 