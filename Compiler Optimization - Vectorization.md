Tags: #compiler-optimizations #performance 

**NOTE:** This was originally written in 2017 and everything below needs to be refreshed.

Requirements for vectorization:
- Loops don't have any dependencies
- Data alignment requirements are met
- Compilers have vectorization enabled

Derived from [Cornell Advanced Computing slides](http://www.cac.cornell.edu/education/training/ParallelFall2012/Vectorization.pdf).

# Loop Dependencies
Four types of loop dependencies: 1) read after write, 2) write after write, 3) write after read, 4) read after read.  The first two are not vectorizable while the last two are.

## Read after Write
Not vectorizable since data needed for a future element is computed by the current loop.  

Sequential computation of the following will always produce a set of outputs different than a vectorized version:
```c
for( i = 1; i< N; i++ )
{
    a[i] = a[i-1] + b[i];
}
```

## Write after Write
Not vectorizable since XXX
```c
for( i = 0; i< N; i++ )
{
    a[i%2] = b[i] + c[i];
}
```

# Write after Read
Anti-dependency.  Vectorizable:
```c
for( i = 0; i< N; i++ )
{
    a[i] = a[i+1] + b[i];
}
```

## Read after Read
Not an actual dependency. Vectorizable:
```c
for( i = 0; i< N; i++ )
{
    a[i] = b[i%2] + c[i];
}
```

# Compilers

Compilers don't vectorize by default and require compilation flags to generate optimized code.

Different compilers require different options:

| Compiler | Optimization Flag | Report Flag | Force Vectorization | Notes |
| --- | --- | --- | --- | --- |
| Intel | `-O2` | `-qopt-report=N` or `-vec-report=N` | `!DEC$ IVDEP` (Fortran) or `#pragma IVDEP` (C/C++) | Unknown version of `icc` tested. |
| GCC | `-O2 -ftree-vectorize` | `-fopt-info-vec` and `-fopt-info-vec-missed` | Unknown | `-O3` turns on vectorization without additional flags |


# Data Alignment
Vectorized data loads and stores typically need to be aligned (**NOTE**: newer Intel architectures are more forgiving for unaligned accesses). 

| Architecture | Byte Boundary |
| --- | --- |
| Opteron, Westmere | 16-bytes (128-bit) |
| Sandybridge | 32-bytes (256-bit) |
| KNL | 64-bytes (512-bit) |

Compilation targeting for a particular architecture should respect this, though specifying a finer alignment via attributes is possible:

| Compiler | Attribute |
| --- | --- |
| Intel | `_declspec( align( 64, 8 ) )` |
| GNU | `__attribute__( (aligned( 64 ) )` |
