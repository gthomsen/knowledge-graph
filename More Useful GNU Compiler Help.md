Tags: #software-engineering #fortran 

Specifying `--help` to a GNU compiler (`gcc`/`g++`/`gfortran`) is not terribly useful as it summarizes programmatic options that control how it is run and wired into the development toolchain.  While it is listed in this output, the `--target-help` option shows something more useful for controlling code generation (similar to Intel's `--help` output):

```shell
$ gfortran --target-help
```

This is useful for determining which architectures are supported by `-march=` or options to generate specific instruction sets.

To show which options are enabled for a given target, the `-Q` option is available:
```shell
$ gfortran -march=native -Q --target-help
```