Tags: #fortran #scientific-computing #software-engineering #unfinished 

# Controlling Stack Allocations
Fortran creates arrays automatically for some types of arrays (i.e. [[FORTRAN77 Features#Explicit-shape Arrays|explicit-shape arrays]] and [[FORTRAN77 Features#Automatic Arrays|automatic arrays]]) at run-time, either as part of explicit definitions in subroutines and functions or as temporary arrays created by an expression.  By default, these are created on the stack though this can [[Exhausting the Stack in Fortran Code|exceed system thresholds and terminate the program]].  

The opinionated correct fix is to allocate large arrays via `allocate()` to explicitly place them on the heap where the only limit is physical memory, or resource constraints (e.g. cgroups).  That said, this requires modifying and testing the code which is not necessarily quick.  In the times where an immediate workaround is needed, compilers typically provide compilation flags which place some/all stack-based arrays onto the heap to avoid heap exhaustion.

## Intel
Intel's `ifort` specifies this via [`-heap-arrays` compilation flag](https://www.intel.com/content/www/us/en/develop/documentation/fortran-compiler-oneapi-dev-guide-and-reference/top/compiler-reference/compiler-options/compiler-option-details/advanced-optimization-options/heap-arrays.html):
```shell
# move all automatic arrays to the heap.
$ ifort -c foo.c -o foo.o -heap-arrays

# move all automatic arrays larger than 10 KiB to the heap.
$ ifort -c foo.c -o foo.o -heap-arrays:10
```

Any array whose size is not known at compile time is moved to the heap, as well as arrays whose size exceed the `<size>` argument to `-heap-arrays:<size>` (specified in KiB).  Omitting `<size>` does presumably moves all arrays to the heap but this is not clear from the documentation (and has not been verified by the author).

## GNU
GNU's `gfortran` specifies a limit to decide where arrays are allocated this via `-fmax-stack-var-size=<N>`:
```shell
# move all automatic arrays larger than 10 KiB to the heap.
$ gfortran -c foo.c -o foo.o -fmax-stack-var-size=10240
```

`<N>` is specified in bytes and defaults to 65535.  See the [official documentation](https://gcc.gnu.org/onlinedocs/gfortran/Code-Gen-Options.html) for additional details.

To unconditionally allocate arrays on the heap, vice the stack, use `-fno-automatic`:
```shell
# move all automatic arrays to the heap.
$ gfortran -c foo.c -o foo.o -fno-automatic
```