Tags: #git 

Submodules are tracked in two places:
1. The submodule directory within the repository
2. The repository's `.gitmodule` file

Adding a submodule will automatically update the `.gitmodule`. 

Check out the submodule and position it to a particular SHA like so:
```shell
$ git submodule add http://github.com/somerepo
$ cd submodule
# NOTE: replace this with a branch/tag as appropriate
$ git checkout SHA
```

Then commit the submodule and the `.gitmodule` file.