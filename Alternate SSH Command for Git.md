Tags: #ssh #git

Controlling SSH configuration when interacting with Git is typically done via `${HOME}/.ssh/config` (e.g. specifying the use of specific keys, or using `ProxyJump` to navigate multiple bastion hosts), though that does not good when one needs to use a different SSH client for the underlying connection.  This can be required when the remote system supplies a custom distribution, perhaps for using Kerberos for authentication. 

In this case, one can either specify an environment variable or the `core.sshCommand` variable in the appropriate `.gitconfig`.

Without specifying either, the first SSH client found in the `PATH` is used and the connection is rejected:
```shell
$ git push remote-with-special-ssh
user@host: Permission denied (gssapi-with-mic).
```

By specifying an alternate SSH client, the connection works:
```shell
$ GIT_SSH=/usr/local/bin/ssh git push remote-with-special-ssh
Counting objects: 29554, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (5190/5190), done.
Writing objects: 100% (29554/29554), 118.46 MiB | 1.13 MiB/s, done.
Total 29554 (delta 23807), reused 29541 (delta 23795)
remote: Resolving deltas: 100% (23807/23807), done.
To host:/home/user/repo.git
 * [new branch]        testing -> testing
updating local tracking ref 'refs/remotes/host/testing'
```

See [`git-config(1)`](https://git-scm.com/docs/git-config) for more details.
