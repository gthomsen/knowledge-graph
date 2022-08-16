Tags: #software-engineering 

Determining the path to the current Makefile (fragment) is useful in larger projects in that it avoids hardcoding locations in too many locations.  

Consider having multiple Makefile fragments that need to add additional dependencies to a top-level Makefile's target.  If the fragments are located in directories different than the top-level Makefile, then the additional dependencies need to have at least relative paths from the top-level.  Without programmatic access to the fragment's location, this path has to be embedded into the fragment which causes friction during maintenance (e.g. renaming the containing directory also requires editing the fragment).

The `MAKEFILE_LIST` variable has each newly parsed Makefile fragment appended to it immediately before executing the fragment.  The following produces an absolute path to the current Makefile (fragment):

```Makefile
MY_CONTAINING_DIRECTORY := $(abspath $(dir $(lastword $(MAKEFILE_LIST))))
```

See the [GNU Makefile manual](https://ftp.gnu.org/old-gnu/Manuals/make-3.80/html_node/make_17.html) for additional details.