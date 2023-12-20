Tags: #fortran #scientific-computing #software-engineering 
XXX: not a comprehensive overview by any stretch, just a collection of painfully learned lessons

# Zero Width Fields
Fortran 95 introduced zero width fields. XXX: back link this

```fortran
integer :: number

number = 1234

write( *, '(I8, I0)' ) number, number
```

Produces the output (XXX: verify this)

```
    1234
1234
```

# Non-Advancing I/O
`write()` statements produce a line break that can be suppressed by specifying `advance='no'` to a `write()` statement.