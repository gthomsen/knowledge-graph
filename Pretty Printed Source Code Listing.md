Tags: #software-engineering #linux #tools 

Generating a PDF of source code for review can be accomplished with `a2ps`.  Code is pretty printed and then can be laid out in a myriad of ways (e.g. landscape with multiple pages of code).

```shell
$ find src/ -name "*.f90"  -print0 | \
      xargs -0 a2ps -2 --delegate no -o - | \
      ps2pdf - output.pdf
```

***NOTE***: There is a way to coax PDF output out of `a2ps` without requiring a separate call to `ps2pdf` though I could not get it to work when specifying an output file via `-o`.  Doing so would generate a file that most PDF viewers would claim was corrupted.

A nice visual synopsis of key features is available from [this Oregon State lecture](https://web.engr.oregonstate.edu/~traylor/ece473/beamer_lectures/a2ps.pdf).