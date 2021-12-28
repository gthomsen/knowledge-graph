Tags: #python #jupyter #benchmarking 

# Line Profiler
Derived from [here](https://jakevdp.github.io/PythonDataScienceHandbook/01.07-timing-and-profiling.html).

Load the extension with:
```
%load_ext line_profiler
```

Profile a particular function (`function_name`) within an expression (`some_expression()`):
```python
%lprun -f function_name some_expression()
```
