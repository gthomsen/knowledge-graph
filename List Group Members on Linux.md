Tags: #linux #utilities 

`getent group` will enumerate the membership of every group on the system.  Use `grep` to find the ones of interest.  Comma-delimited membership.

```shell
$ getent group | grep groupname
groupname:x:member1,member2,member3
```