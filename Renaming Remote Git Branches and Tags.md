Tags: #git 

Renaming branches and tags that have been pushed to a remote repository involves deleting the original and pushing the new.  Branches and tags have different syntax for the same operation.

Derived from these Stack Overflow posts:
- [Renaming branches remotely in Git](https://stackoverflow.com/questions/4753888/renaming-branches-remotely-in-git)
- [How do you rename a Git tag?](https://stackoverflow.com/questions/1028649/how-do-you-rename-a-git-tag)

# Branches

```shell
# create a new branch from the old.
$ git branch new-branch-name origin/old-branch-name

# create the new upstream branch.
$ git push origin --set-upstream new-branch-name

# delete the old local branch.
$ git branch -D old-branch-name

# delete the old upstream branch.
$ git push origin :old-branch-name
```

# Tags
```shell
# create a new tag using the commit the old tag points to.
#
# NOTE: if 'old-tag-name' refers to a tag object, use 'old-tag-name^{}' instead.
#       see below for details.
#
$ git tag new-tag-name old-tag-name

# remove the old local tag.
$ git tag -d old-tag-name

# remove the old upstream tag and push the new upstream tag.
$ git push origin new-tag-name :old-tag-name
```

***NOTE:*** Care needs to be taken with tags objects as they are different than lightweight tags.  Tag objects have additional information (annotations, messages, GPG signatures, etc).  If `old-tag-name` refers to a tag object, then use `old-tag-name^{}` instead of `old-tag-name` when creating `new-tag-name`.

Other users should also prune references to removed tags with the following:
```shell
# remove remote-tracking references that no longer exist on the remote.  without this,
# the old tag will remain in working copies that previous contained it.
$ git pull --prune --tags
```