Tags: #fortran #mpi #scientific-computing 

Intel's Classic compilers (`icc`, `icpc`, and `ifort`) are slowly being deprecated in favor of the oneAPI set of compilers (`icx`, `icpx`, and `ifx`).  Utilizing them for serial builds is straight forward - simply specify the appropriate compiler where ever appropriate.  Specifying them for use with Intel's MPI requires a little effort since `mpiicc`, `mpiicpc`, and `mpiifort` are not replaced with oneAPI variants.  Two approaches appear to exist: 1) specifying paths as arguments to MPI wrappers and 2) specifying paths as environment variables.

Derived from EasyBuild [issue #4056](https://github.com/easybuilders/easybuild-framework/issues/4056) and [issue #4062](https://github.com/easybuilders/easybuild-framework/pull/4062).

# MPI Wrapper Arguments
The following compiler arguments specify compiler locations to the MPI wrappers.

| MPI Wrapper | Wrapper Argument | Default (Legacy) Value | New Value |
| --- | --- | --- | --- |
| `mpiicc` | `-cc` | `icc` | `icx` |
| `mpiicpc` | `-cxx` | `icpc` | `icpx` |
| `mpiifort` | `-fc` | `ifort` | `ifx` |

```shell
$ mpiifort --version
ifort (IFORT) 2021.6.0 20220226
Copyright (C) 1985-2022 Intel Corporation.  All rights reserved.

$ mpiifort --version -fc=ifx
ifx (IFORT) 2022.1.0 20220316
Copyright (C) 1985-2022 Intel Corporation. All rights reserved.
```

# MPI Environment Variables
The following table shows how environment variables specify compiler locations to the MPI wrappers.

| MPI Wrapper | Environment Variable | Default (Legacy) Value | New Value |
| --- | --- | --- | --- |
| `mpiicc` | `I_MPI_CC` | `icc` | `icx` |
| `mpiicpc` | `I_MPI_CXX` | `icpc` | `icpx` |
| `mpiifort` | `I_MPI_F90` | `ifort` | `ifx` |

For example:
```shell
$ mpiicc --version
icc: remark #10441: The Intel(R) C++ Compiler Classic (ICC) is deprecated and will be removed from product release in the second half of 2023. The Intel(R) oneAPI DPC++/C++ Compiler (ICX) is the recommended compiler moving forward. Please transition to use this compiler. Use '-diag-disable=10441' to disable this message.
icc (ICC) 2021.7.0 20220726
Copyright (C) 1985-2022 Intel Corporation.  All rights reserved.

$ I_MPI_CC=icx mpiicc --version
Intel(R) oneAPI DPC++/C++ Compiler 2022.2.0 (2022.2.0.20220730)
Target: x86_64-unknown-linux-gnu
Thread model: posix
InstalledDir: /software/intel-compilers/2022.2.0/compiler/2022.2.0/linux/bin-llvm
Configuration file: /software/intel-compilers/2022.2.0/compiler/2022.2.0/linux/bin/icx.cfg
```
