Tags: #fortran #scientific-computing 

While modern Fortran ([[Fortran90 Features|Fortran90]], [[Fortran95 Features|Fortran95]], [[Fortran 2003 Features|Fortran 2003]], [[Fortran 2008 Features|Fortran 2008]], etc) provide the ability to explicitly control memory allocations on the heap via `allocate()`, a number of seemingly innocuous language constructs result in stack usage.  For large arrays, this can result in program termination (via SIGSEGV) on lines of code that do not explicitly allocate data, like the following:

```fortran
    ...
    real(kind=dp), parameter :: zero = 0.0_dp          
    real(kind=dp), target    :: dudx(N), dudy(N), dudz(N)
    
    dudx = zero    ! potential stack exhaustion when N is large!
    dudy = zero
    dudz = zero
    ...
```

Depending on the size of `N` and the call stack that leads to executing the above `block` it may run just fine. Or it may segfault as `dudx`'s array is accessed after being allocated via overcommit (read: where you have sufficient virtual memory but not physical memory to back it).

The correct fix is usually explicit allocation of large arrays via `allocate()`, though this may be difficult (i.e. lots of code to update) or impossible (i.e. working with externally supplied code) so workarounds exist to change the stack limit.  First one must diagnose the issue to confirm stack exhaustion is the culprit and then a decision must be made regarding the type of fix.

# Diagnosing the Issue
Any of the following are true then the underlying issue is likely stack exhaustion:
1. The crash goes away completely when stack limit is removed via `ulimit -s unlimited`
2. The crash goes away, or moves, when a different number of threads are used.  Varying thread counts can change the overall stack size used as a fixed size of N bytes now must be shared amongst M threads.  This is particularly true for OpenMP and large arrays declared as `PRIVATE` in their sharing clause.
3. The crash goes away, or moves, when a different compiler or memory allocator is used
4. The array in question is [[FORTRAN77 Features#Explicit-shape Arrays|explicit-shape]] or an [[FORTRAN77 Features#Automatic Arrays|automatic]] array.  These array types may be allocated on the stack which contributes to the stack threshold being exceeded.

## Addressing the Issue
There is no one right answer for addressing this issue, though the best approach is typically converting the arrays to be `allocatable` and then explicitly managing their memory via `allocate()`/`deallocate()`.  Unfortunately, this requires the most work as it is not an automatic change which, for large code bases, can require a fair amount of time.  That said, following coding standards and a KISS mentality this should be done from the beginning of development.

If a quick fix is required, then running without a stack size limit can be accomplished like so:
```shell
$ ulimit -s unlimited
```
Raising the threshold is only done for the current shell and needs to be added to job scripts or login scripts (NOTE: this is rarely the correct fix as it affects **EVERYTHING** run by the user).

A more controlled, temporary fix can be made via compiler flags to [[Fortran Compiler Support#Controlling Stack Allocations|control which allocations are stack-based vs heap-based]] on a file-by-file basis:
```shell
$ ifort -c foo.c -o foo.o -heap-arrays
$ gfortran -c foo.c -o foo.o -fno-automatic
```
This can be made even more granular by specifying explicit size limits to transition from the stack to the heap, though is compiler specific and is often confusing (which flag do you use, what is the threshold's units).

See [here for additional view points](https://groups.google.com/g/comp.lang.fortran/c/9_0q0dBRzpk).
