Tags: #software-engineering #fortran #scientific-computing 

End of file (EOF) is handled separate from an I/O error in Fortran.  Older, non-compliant compilers may treat them as the same, though specifying the `end` **AND** `err` parameters to `read()` is the correct way to distinguish and handle the conditions.

Once EOF or an error are encountered, all variables being read are considered undefined.