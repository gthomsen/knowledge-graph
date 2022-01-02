Tags: #emacs 

The `align` package provides a framework for aligning text about common points (e.g. about a `=` in an expression).  Should a mode not do the right thing, the most likely culprit is how the rules' `align-region-separate` is set.  This should almost always be set to `entire`, though `largest` is also suitable (though not implemented as of 2017/02/03).