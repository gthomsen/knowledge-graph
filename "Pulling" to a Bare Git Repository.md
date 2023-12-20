Tags: #git 

Pulling requires a working copy, so fetching changes from a remote is required when working with a bare Git repository.

```shell
# XXX: unclear why branch_name needs to be duplicated.
$ git fetch remote branch_name:branch_name
```