Tags: #software-engineering #python 

Flattening a list of lists is trivial with [`itertools.chain()`](https://docs.python.org/3/library/itertools.html#itertools.chain).  It creates an iterator that returns each of the contents of iterable supplied.

```python
import itertools

lists_of_lists = [["a", "b"], ["c"]]

# equivalent to list( ["a", "b", "c"] ).
flattened_list = list( itertools.chain.from_iterable( list_of_list ) )
```