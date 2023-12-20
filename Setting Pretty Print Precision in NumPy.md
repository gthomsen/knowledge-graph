Tags: #scientific-computing #python 

Changing the precision when printing NumPy arrays is done via `.set_printoptions()`:
```python
previous_print_options = numpy.get_printoptions()

numpy.set_printoptions( precision=2 )
...

numpy.set_printoptions( precision=previous_print_options["precision"] )
```

Suppressing scientific notation is done like so:
```python
numpy.set_printoptions( suppress=True )
```

A context manager interface is also available to avoid having to get and restore the previous options:
```python
with numpy.printoptions( precision=10 ):
    print( numpy_array )
```