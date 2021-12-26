Tags: #linux

# Versions
Query the system's version:
```shell
$ lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 20.04.3 LTS
Release:        20.04
Codename:       focal
```

Versions are of the form `YY.MM` and have a codename (e.g. `hirsute`).  Multiple Ubuntu releases come from the same [[Debian]] version (e.g. `bullseye`).

Selection of versions seen:
- 21.10: impish (bullseye)
- 21.04: hirsute (bullseye)
- 20.04: focal (bullseye)
- 19.04: disco (buster)
- 18.10: cosmic (buster)
- 18.04: bionic (buster)
- 16.04: xenial (stretch)
- 14.04: trusty (jessie)

[Ask Ubuntu](https://askubuntu.com/questions/445487/what-debian-version-are-the-different-ubuntu-versions-based-on)has an updated list

The contents of `/etc/debian_version` tell you the version of Debian. 

