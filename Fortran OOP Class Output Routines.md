Tags: #fortran #unfinished 

Fortran 2003 introduced user-derived types and generics, which supports the ability to write out an object via a type method.  This is done via a `generic :: write(formatted) => type_write_method` attribute within a type declaration.  The following code demonstrates how to declare a type that uses this functionality.

```fortran
type, public :: user_type
...

procedure :: custom_write
generic   :: write(formatted) => custom_write

end type user_type

interface
    module subroutine custom_write( this, a_unit, a_iotype, a_vlist, a_iostat, a_iomsg )
        class(user_type), intent(in) :: this
        integer, intent(in)          :: a_unit
        character(*), intent(in)     :: a_iotype
        integer, intent(in)          :: a_vlist(:)
        integer, intent(out)         :: a_iostat
        character(*), intent(inout)  :: a_iomsg
    end subroutine custom_Write
end interface
```