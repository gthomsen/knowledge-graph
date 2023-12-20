Tags: #macos #utilities 

The `chflags` utility can make files immutable on MacOS which prevents modification regardless of the discretionary access controls (DAC) in place.  Immutability can be enforced for user-modification (`uchg`) or privileged-modification (`schg`):

```
$ rm foo.txt
$ touch foo.txt
$ ls -la foo.txt
-rw-r--r--  1 user  staff  0 Jun 30 17:04 foo.txt
$ chflags uchg foo.txt
$ touch foo.txt
touch: foo.txt: Operation not permitted
```