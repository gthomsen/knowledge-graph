Tags: #git #software-engineering 

Pushing a subset of local commits to an upstream repository is useful if some of a branch's work is ready to be shared, but not all of them.  Naively specifying the SHA1 of the last commit to push from a branch does not work, as one must specify a reference for both the local (the last local commit) and remote (the name of the branch).

Consider the following sequence of commits (going backwards from `HEAD`):
1. `f7dfc30` - Commit to ***NOT*** push
2. `67c6852` - First commit to push
3. `15c2df2` - Second commit to push
4. `eb7106e` - Most recent commit in the remote (`(origin/branch_name)`)

The following pushes just commits `67c6852` and `15c2df2`, but not `f7dfc30`:

```shell
$ git push -n origin branch_name~1:branch_name

# the following also works if branch_name~1's SHA1 is "67c6852".
# git push -n origin 67c6852:branch_name
```
