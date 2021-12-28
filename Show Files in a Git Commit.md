Tags: #git

Show a commit's message and the paths modified:
```shell
$ git show --name-only <commit>
```

The commit message can be condensed via `--oneline`:
```shell
$ git show --oneline --name-only HEAD
78c6e81 (HEAD -> main, origin/main) Topic: PDF Regular Expression Search Support Update
Dockerfile
README.md
```

The status of each file can be requested via `--name-status` instead of `--name-only`:
```shell
$ git show --oneline --name-status HEAD
78c6e81 (HEAD -> main, origin/main) Topic: PDF Regular Expression Search Support Update
M       Dockerfile
M       README.md
```
