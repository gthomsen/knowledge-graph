Tags: #git 

**Be VERY CAREFUL if working on revisions that have been pushed.**

Setting the `GIT_AUTHOR_DATE` or `GIT_COMMITTER_DATE` variables during a commit will use a date other than now.  

The date format is described in [`git-commit(1)`](https://mirrors.edge.kernel.org/pub/software/scm/git/docs/git-commit.html#_date_formats).  ISO 8601 is the easier format to remember (e.g. `2021-12-27T21:45:13`).

Setting these during an interactive rebase (when `edit`'ing revisions) works.

This Stack Overflow [post](https://stackoverflow.com/questions/3895453/how-do-i-make-a-git-commit-in-the-past) has more complicated approaches.  Doing something like [[Change Author or Email in Git Commits|how you change the author of a commit]] is likely overkill.