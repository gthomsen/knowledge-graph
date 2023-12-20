Tags: #python #software-engineering #matplotlib 

# Removing Unused Subplots

Creating a grid of subplots via `matplotlib.pyplot.subplots()` causes them to be rendered as empty unless filled with a plot or removed.  Removing is done by calling the axis' `.remove()` method:
```python
    # we don't have a 6th plot to show, so remove the axis so it isn't rendered
    # as empty.
    ax_h[1][2].remove()
```