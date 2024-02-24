Tags: #fortran 

# Left and Right Justification

The `T<N>` descriptor adjusts the output of the next field to start at column `<N>`.

```fortran
! Produces: "Left           1234"
write( *, "(A,T15,I0)" ) "Left", 1234
! Produces: "           Left1234"
write( *, "(A15,I0)" ) "Right", 1234
```

# Derived Types

XXX: `DT`

See also [[Formatting Floating Point Values in Fortran Output]].