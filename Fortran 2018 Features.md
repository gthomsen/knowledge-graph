Tags: #software-engineering #fortran 

# Assumed Types
Assumed types are similar to [[Fortran 2003 Features#Unlimited Polymorphic Types|Fortran 2003's unlimited polymorphic types]] (i.e. variables whose type is `class(*)`), though are specified as `type(*)`.  While assumed type arguments are type compatible with anything, they cannot be used with `select type` and primarily exist for interfacing with non-Fortran code.  One can think of these as variables with no type, similar to C's `void`, but they acquire their type information from their effective argument.

Typically one will use the `ISO_C_BINDING`'s `c_loc()` intrinsic, along with `c_f_pointer()`, to translate an assumed type argument into something that has a usable Fortran type.

See the "No Limits" section from [this Dr. Fortran post](https://stevelionel.com/drfortran/2020/06/30/doctor-fortran-in-not-my-type/) for additional details.