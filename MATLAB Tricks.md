Tags: #matlab 

# Deleting an Entry From a Cell Array
Cell arrays ability to hold anything makes deleting entries non-intuitive.

Use the array index syntax to delete an entry:
```matlab
cell_array(index) = [];
```

And use the cell index syntax to assign an empty array:
```matlab
cell_array{index} = [];
```