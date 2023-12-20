Tags: #linux #ubuntu 

Systems occasionally get renamed and the following provides a CLI-based approach on Ubuntu 22.04 systems:
```shell
$ sudo hostnamectl set-hostname <newname>
```

While `hostnamectl` takes care of updating the relevant configuration files it does not update `/etc/hosts`, so that needs to be updated:
```shell
$ cat /etc/hosts
127.0.0.1 localhost
127.0.1.1 <oldname>

$ sudo vim /etc/hosts
... replace <oldname> with <newname> ...
```