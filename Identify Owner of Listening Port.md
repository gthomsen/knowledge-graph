Tags: #tools 

# Linux
Tags: #linux 

Linux's `netstat` (part of net-tools) can print the name of the process that owns a particular socket.  The 7th column printed when process names are requested (`-p` option) specifies both the PID and the name:
```shell
$ netstat -ntaup | grep Xvnc
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
tcp        0      0 0.0.0.0:5901            0.0.0.0:*               LISTEN      2081922/Xvnc
tcp        0      0 0.0.0.0:6001            0.0.0.0:*               LISTEN      2081922/Xvnc
tcp        0      0 0.0.0.0:6101            0.0.0.0:*               LISTEN      2081922/Xvnc
tcp6       0      0 :::6101                 :::*                    LISTEN      2081922/Xvnc
```

# MacOS
MacOS's `netstat` does not provide the details as on Linux.  The following will confirm that something is listening on a particular port but will not provide the owner's PID:

```shell
$ netstat -nav | grep 8888
tcp46      0      0  *.8888                 *.*                    LISTEN      131072 131072  20770      0 0x0100 0x00000006
```

`lsof` can provide the command, PID, and user:

```shell
$ $ lsof -n -i:8888
COMMAND     PID     USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
com.docke 20770 username  176u  IPv6 0x8247e33d3f2d8ff3      0t0  TCP *:8888 (LISTEN)
```