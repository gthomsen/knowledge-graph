Tags: #git

The `show` subcommand shows objects in a commit, whether those are names in the tree of files in the commit, the contents of a file, or the status of one or more files.

# Showing Status

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

# Showing Files

The general format for showing a specific file is:
```shell
$ git show <commit>:<path>
```

***NOTE:*** `<path>` is a path relative to the repository's base!  Do not supply an absolute path or something relative to the current (non-repo-base) directory!