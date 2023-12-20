Tags: #fortran #tools #software-engineering #linux 

Intel compilers (`icc`, `icpc`, `ifort`, etc) support coverage instrumentation via the `-prof-gen=srcpos` compilation option.  Running the instrumented executables generates `.dyn` files which are combined via `profmerge` to generate `.dpi` and `.spi` files.  The `.dpi` and `.spi` files can be processed with `codecov` to generate `CODE_COVERAGE.HTML` and corresponding files (the `CodeCoverage/` directory).

The above roughly translates to the following commands:

```shell
$ ifort -prof-gen=srcprof foo.f90 -o foo.x
$ ./foo.x
... <prefix>_<pid>.dyn is generated ...
$ profmerge
1. block count = 60, 2. block count = 58
$ codecov
Intel(R) C++/Fortran Compiler Classic code-coverage tool, Version 2021.6.0 Build 20220226_000000
Copyright (C) 1985-2022 Intel Corporation.  All rights reserved.

Progress: 10% .. 20% .. 30% .. 40% .. 50% .. 60% .. 70% .. 80% .. 90% .. 100%
$ ls -ld CODE_COVERAGE.HTML Code_Coverage
-rw-r--r--  1 user user     510 Jan 29 16:23  CODE_COVERAGE.HTML
drwxr-xr-x  2 user user  131072 Jan 29 16:23  CodeCoverage
```

Control over the generated HTML reports is done via options passed to `codecov`.