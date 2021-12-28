Tags: #git 

**Be VERY CAREFUL if working on revisions that have been pushed.**

`git filter-branch` can re-write history for all branches and tags.  

From this Stack Overflow [post](https://stackoverflow.com/questions/750172/how-to-change-the-author-and-committer-name-and-e-mail-of-multiple-commits-in-gi)'s [answer](https://stackoverflow.com/a/1320317) (CC BY-SA 4.0), though be sure to change the values set for `OLD_EMAIL`, `CORRECT_NAME`, and `CORRECT_EMAIL` :
```shell
$ cat fix-email.sh
#!/bin/sh

git filter-branch --env-filter '

OLD_EMAIL="old@email.com"
CORRECT_NAME="New Name"
CORRECT_EMAIL="new@email.com"

if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi

if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi

' --tag-name-filter cat -- --branches --tags
```