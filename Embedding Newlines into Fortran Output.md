Tags: #fortran #software-engineering 

The following uses slash editing to generate an empty line between two lines of output, using a single `write()` call:
```fortran
write( *, "(A,/,/,A)" ) "First line", "Second line"
```

The above generates:
```
First line

Second line
```

Slash edit descriptors can have a repeat count so the above code can be simplified like so:
```fortran
write( *, "(A,2/,A)" ) "First line", "Second line"
```

Slash edit descriptors appear to not be defined when writing to an internal file (read: character array) so the `new_line()` intrinsic must be used instead:

```fortran
character(len=100) :: fixed_string

write( fixed_string, "(A,A,A,A)" ) "First line", new_line( "a" ), new_line( "a" ), "Second line"
write( *, "(A)" ) fixed_string
```