Tags: #software-engineering #fortran 

Allocatable objects can be initialized during the `allocate()` in a process called _sourced allocations_.  This was introduced in Fortran 2003.

```fortran
! allocate some_array according to its dimensions and initialize it to 0.0.
allocate( some_array, source=0.0 )
```

**NOTE:** The shape is taken from the target and **NOT** the source.

Multiple objects can be allocated and initialized at once in Fortran 2008:
```python
! allocate one_array and another_array according to their dimensions
! and initialize them to 0.0.
allocate( one_array, another_array, source=0.0 )
```

`source` can be another object:
```fortran
allocate( some_array, source=initialized_array )
```

**NOTE:** It is undefined behavior when using sourced allocations with an uninitialized source object.