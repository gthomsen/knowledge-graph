Tags: #software-engineering 

| Compiler | Command | Notes |
| ---- | ---- | ---- |
| GNU gfortran | `gfortran -cpp -E -dM - < /dev/null \| sort` | Provides each symbol's `#define` directive. |
| Intel ifort | `ifort -fpp -E /dev/null -dryrun 2>&1 \| grep -E '^ *-D'` | Provides each symbol's definition as found on the command line. |
| Intel ifx | `ifx -fpp -E /dev/null -dryrun 2>&1 \| grep -E '^ *-D'` | Provides each symbol's definition as found on the command line. |
| Cray Fortran | Unknown.  | Documentation on `crayftn`'s preprocessor is sparse.  It does not appear that additional arguments can be supplied to the preprocessor (`ftnfe`) to get the final list of symbols defined like the C and C++ compilers can (e.g. `-Wp,-list_final_macros` or `cc -dM -E -x c /dev/null`) . |

Additional flags to the command lines above (e.g. `-fopenmp` or `-qopenmp` for enabling OpenMP) may modify the output of each compiler.

All of the above commands will produce symbols present for C and C++ compilers with little to no modification.