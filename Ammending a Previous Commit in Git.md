Tags: #git 

**Be VERY CAREFUL if working on revisions that have been pushed.**

Ammending one or more previous commits can be done with a combination of `git rebase` and `git reset --soft`:

```shell
$ git rebase -i <commit>
... 'edit' the target commits ...
$ git reset --soft HEAD~
... do what needs to be done, then commit ...
```
