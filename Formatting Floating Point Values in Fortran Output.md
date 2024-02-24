Tags: #fortran #software-engineering #unfinished 

Formatting floating point values in Fortran record output (using `write()`) requires care and knowledge about the range of values encountered to get formatting correct.  There are five different edit descriptors that handle floating point values: `G`, `EN`, `ES`, `E`, and `F`.  Each has different behavior depending on the magnitude of the value printed and the width requested for output.  The following highlights some of differences:
```fortran
real :: floating_point

floating_point = 32.1234837

write( *, "(A,G0.1)" )  "G ",  floating_point
write( *, "(A,EN0.1)" ) "EN ", floating_point
write( *, "(A,ES0.1)" ) "ES ", floating_point
write( *, "(A,E0.1)" )  "E ",  floating_point ! width of 0 not allowed!
write( *, "(A,F0.1)" )  "F ",  floating_point

floating_point = 32034.1234837

write( *, "(A,G0.1)" )  "G ",  floating_point
write( *, "(A,EN0.1)" ) "EN ", floating_point
write( *, "(A,ES0.1)" ) "ES ", floating_point
write( *, "(A,E0.1)" )  "E ",  floating_point ! width of 0 not allowed!
write( *, "(A,F0.1)" )  "F ",  floating_point
  
floating_point = .3234234

write( *, "(A,G0.1)" )  "G ",  floating_point
write( *, "(A,EN0.1)" ) "EN ", floating_point
write( *, "(A,ES0.1)" ) "ES ", floating_point
write( *, "(A,E0.1)" )  "E ",  floating_point ! width of 0 not allowed!
write( *, "(A,F0.1)" )  "F ",  floating_point
write( *, "(A,F5.1)" )  "F ",  floating_point
```

GNU gfortran 7.5 produces:
```
G 0.3E+2
EN 32.1
ES 3.2E+1
E 0.3E+2
F 32.1

G 0.3E+5
EN 32.0E+3
ES 3.2E+4
E 0.3E+5
F 32034.1

G 0.3
EN 323.4E-3
ES 3.2E-1
E 0.3
F .3
F   0.3
```

Observations of the above:
- `G` does not normalize the leading digit to be non-zero and incurs mental friction to read it
- `EN` moves the decimal point so the exponent is always a multiple of 3.  Does not produce a consistent format (without a larger width to accommodate) when there is a wide range of values.
- `ES` normalizes the leading digit and always prints the exponent regardless of magnitude
- `E` does not normalize the leading digit and omits the exponent when it isn't necessary, leading to inconsistent formatting when there is a wide range of values
- `F` does not guarantee a leading zero will be output if width detection (`F0`) is used, but typically will produce the zero when a fixed width is requested (`F<N>.1`) which requires explicit knowledge of the range of values

# Leading Zeros in the `F` Descriptor are Implementation Dependent
[Intel Forums Post - "Leading zeros in the f0.x format descriptor"](https://community.intel.com/t5/Intel-Fortran-Compiler/Leading-zeros-in-the-f0-x-format-descriptor/td-p/1175148)
