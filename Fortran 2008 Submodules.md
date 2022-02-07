Tags: #software-engineering #fortran #scientific-computing 

Submodules were introduced in Fortran 2008 allowing for single-ancestor inheritance from parent modules or submodules.

# Anatomy of a Submodule
Each submodule is comprised of two things:
1. Specification - what it "offers" to the world
2. Subprogram - implementation for some of what it offers

The subprogram is everything after the `CONTAINS` statement and may be  specified separately from the specification.  It can also provide definitions for ancestor interfaces.

# Access Scope
Submodules have public access to all of their ancestor modules procedures, 
interfaces, and derived types.

Local variables are only accessible within the current submodule and descendant submodules.

# Restrictions of Submodules
Submodule names cannot be shared with other global entities.

# Dependencies Introduced by Submodules
Detecting dependencies between translation units is challenging because each unit must be parsed to determine:
1. Which `MODULE`s or `SUBMODULE`s are contained
2. Which `MODULE`s or `SUBMODULE`s are `USE`d

Manually tracking these dependencies is brittle and error prone.  [[Building Fortran Applications with CMake|Build systems like CMake]] are better suited for this.

# References
- [Think Geek post titled "Fortran and modules"](https://thinkingeek.com/2019/03/10/fortran-and-modules/) gives a gentle introduction into Fortran modules and how they related to C++20 modules.

# Random Details
Trivia for cocktail parties:
- Submodules were introduced in Fortran 2003 but were deferred to the 2008 standard.
- The C++20 modules implementation has an analog called "Module Implementation Partitions".