Tags: #utilities 

`apt-get install` will prompt the user for input as necessary, which is a no-no for unattended installations (i.e. systems or container images).  `DEBIAN_FRONTEND=noninteractive` will prevent `apt-get` from soliciting input.

Installing the timezone database asks the user for geographic information about the system:
```shell
$ sudo apt-get install tzdata
XXX: prompts for location
```

Non-interactive installations select a suitable default (UTC in the case of `tzdata`):
```shell
$ sudo sh -c "DEBIAN_FRONTEND=noninteractive apt-get install tzdata"
```