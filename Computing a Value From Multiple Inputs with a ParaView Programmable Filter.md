Tags: #paraview #python #scientific-computing 

Computing a value from multiple inputs in a Paraview programmable filter requires accessing the inputs via `inputs[N]` and appending a VTKArray to the `output` variable:

```python
from paraview.vtk.numpy_interface import dataset_adapter as dsa

dataset_name = "u"

golden = inputs[0].PointData[dataset_name]
result = inputs[1].PointData[dataset_name]

ratio = result / golden
output.PointData.append( dsa.VTKArray( ratio ), "ratio" )
```

Derived from this [Stack Overflow answer](https://stackoverflow.com/a/46430959).