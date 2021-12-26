Tags: #linux #tools 

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