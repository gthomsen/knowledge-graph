Tags: #scientific-computing #software-engineering 

OpenMP capable compilers define the `_OPENMP` symbol which specifies the `YYYYMM` date of the latest version of the standard supported.

| OpenMP Version | Specification Date |
| ---- | ---- |
| 1.0 | 199810 |
| 2.0 | 200203 |
| 2.5 | 200505 |
| 3.0 | 200805 |
| 3.1 | 201107 |
| 4.0 | 201307 |
| 4.5 | 201511 |
| 5.0 | 201811 |
| 5.1 | 202011 |
| 5.2 | 202111 |

Specification dates are integers that are ordered so a particular specification can be targeted at compile time (e.g. `#if _OPENMP >= 201511` is only true for compilers supporting OpenMP 4.5 and newer).  It can be useful [[Printing Preprocessor Symbols Defined by the Fortran Compiler|to print the preprocessor symbols defined]] to see what a particular compiler supports.

It's worth noting that some versions of Intel's ifort/ifx compilers will report a non-existent specification date, `201611`.  Intel's [oneAPI documentation lists oneAPI versions that support OpenMP](https://www.intel.com/content/www/us/en/developer/articles/technical/openmp-features-and-extensions-supported-in-icx.html) 4.5 and newer.

Derived from this [Stack Overflow post](https://stackoverflow.com/a/34322820).