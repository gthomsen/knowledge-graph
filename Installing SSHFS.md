Tags: #macos #ssh

Install MacFUSE.  

Update System Preferences to allow system extensions from known developers:
1. Shutdown
2. Hold the Power button and change the system
3. Select Allow Known Developers

Install SSHFuse.

Mount a directory over SSH:
```shell
$ sshfs user@host:/path/on/server /path/on/client
```

`sshfs` supports alternate ports via `-p <port>`.