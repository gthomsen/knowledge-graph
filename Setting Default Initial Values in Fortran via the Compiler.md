Tags: #scientific-computing #fortran #software-engineering 

Using uninitialized values in computations is not a great thing to do though for complex programs that pass multi-dimensional arrays around (and ${DIETY} help you if pointer/aliasing tricks are involved) this can be difficult to verify without extra work.  Fortunately, most Fortran compilers provide a means to initialize values to sentinels that can be easily checked for (e.g. NaN or -999).

Derived from the [gfortran documentation](https://gcc.gnu.org/onlinedocs/gfortran/Code-Gen-Options.html), this [Stack Overflow post](https://stackoverflow.com/questions/31971836/having-parameter-constant-variable-with-nan-value-in-fortran) on creating a constant NaN, and the [Cray Fortran compiler options](https://support.hpe.com/hpesc/public/docDisplay?docId=a00115296en_us&page=Fortran_Command-line_Options.html) documentation.

# Floating Point Values
In the context of the options below, floating point values refer to `real` variables as well as both real and imaginary components of `complex` variables.

| Vendor | Compiler | Option | Notes |
| --- | --- | --- | --- |
| Cray | `crayftn` | `-e i` | Initializes all scalar and array floating point values, regardless of the array's location (i.e. heap vs stack) |
|  GNU | `gfortran` | `-finit-real=snan` | Does *NOT* apply to `allocate()`'d arrays!  `snan` can be replaced with `nan` (non-signalling), `inf`/`-inf` or `zero`.
| Intel | `ifort`, `ifx` | `-init=arrays -init=snan` | Initializes all scalar and array floating point values, regardless of the array's location (i.e. heap vs stack) |

A huge caveat here - GNU gfortran does not initialize `allocate()`'d arrays, only scalar and assumed-size arrays!  This makes it significantly more challenging to catch bugs in a debug release as large arrays will typically be `allocate()`'d.

# Integers
Integers can get default values as well.  Note that I haven't used this directly, just leaving an incomplete version here as a breadcrumb.

| Vendor | Compiler | Option | Notes |
| --- | --- | --- | --- |
| Cray | `crayftn` | | |
| GNU | `gfortran` | `-finit-integer=<value>` | Sets all integers to `<value>`|
| Intel | `ifort`, `ifx` | | |

