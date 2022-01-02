Tags: #fortran #software-engineering 

Unsurprisingly, exit codes were not standardized until Fortran 2008. The `stop` statement does ***NOT*** actually return an exit code, but rather prints its argument (which is a 5-character string). Some implementations will also exit with this value if it's numeric.

The `error stop` statement does take an exit code and passes it back to the OS, though is Fortran 2008-specific.