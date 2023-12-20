Tags: #scientific-computing #python #debugging #jupyter 

# Interactive Debugging
PDB cannot be directly used from within a Jupyter notebook, so the following is required to provide an entry point into the debugger:
```python
from IPython.core.debugger import set_trace
```

Call `set_trace()` inside a cell (either in a defined function or directly within a cell) and execution is then controlled by a text field tied to PDB.

# Post-mortem Debugging
Add `%debug` in the cell after an exception has been raised to debug.