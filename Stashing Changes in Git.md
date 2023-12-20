Tags: #git 

Stashing partial changes via `git stash` is done differently depending on whether one wants to specify a message or not.  

**NOTE:** Both approaches only take file paths. Specifying a directory will be ignored and all available changes are stashed.

Stashing without a message:
```shell
$ git stash -- filename.ext [...]
```

Stashing with a message:
```shell
$ git stash push -m "message goes here" filename.ext [...]
```