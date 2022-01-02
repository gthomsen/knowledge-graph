Tags: #emacs #matlab

**NOTE:** This may be outdated.

Etags doesn't have direct support for MATLAB or Octave so custom regexp's need to be supplied.  Here is one that indexes all functions (skips global variable declarations):
```shell
$ etags --language=none --regex='/function\(\(.*\)=\)?[    ]*\([^  ]*\)([  ]*\(.*\)[   ]*)/\3/' *.m
```
