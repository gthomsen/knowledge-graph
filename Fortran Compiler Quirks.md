Tags: #fortran #software-engineering #scientific-computing 

Different compilers have different levels of Fortran maturity.  Below are a collection of notable quirks.

# gfortran
## Uninitialized Variables
gfortran has not been able to properly identify (potentially) uninitialized variables for a while.  See [Bugzilla #77504](https://gcc.gnu.org/bugzilla/show_bug.cgi?id=77504) for a six year run of reports, along with various duplicate bugs associated to the topic.

It is particularly verbose when assigning the result of a function whose return value is allocatable **and** [[Fortran 2003 Features#Reallocations|object reallocation]] occurs during assignment.  Spurious warnings occur when code similar to the following is encountered:
```fortran
function allocate_objects( number_objects ) result( new_objects )
    integer, intent(in)          :: number_objects
    type(some_type), allocatable :: new_objects(:)

    allocate( new_objects(number_objects) )
end function allocate_objects

! NOTE: some_type's definition is omitted for brevity.
type(some_type), allocatable :: a(:), b(:), c(:)

a = allocate_objects( 3 )
b = allocate_objects( 9 )

! allocates storage for c (possibly transferring ownership from a).
c = a

! reallocation of c's storage.
c = b
```

Note that `-Wuninitialized` and `-Wmaybe-uninitialized` is turned on when `-Wall` is enabled, so consider `-Wall -Wno-uninitialized -Wno-maybe-uninitialized` instead (**NOTE:** this may be incorrect and that `-Wextra` enables these, though the fix is the same).

# Observed Undefined Behavior with Pointer Intents
The Fortran 2003 specification allows [[Fortran 2003 Features#Pointer Intents|pointers to have `intent` attributes]], though it is a specifier on the pointer itself and ***NOT*** what it points to.  As a result, pointers marked as `intent(out)` have an undefined association which means it does not have to point to what it did in the caller's scope.

It appears that gfortran (versions 7.5 through 11.3) does not modify a pointer's association under normal circumstances, while ifort (2021.4-2021.6) does.  Thus, this broken code appears to be correct when compiled with gfortran but "mysteriously" breaks under ifort:

```fortran
subroutine compute_with_array( array_pointer )
    real, dimension(:, :, :), pointer, intent(out) :: array_pointer

    ! UNDEFINED: array_pointer is not guaranteed to point to anything
    ! regardless of its status in the caller's scope.
    array_pointer(1, 1, 1) = 0.0
end subroutine
```