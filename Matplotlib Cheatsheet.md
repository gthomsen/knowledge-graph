Tags: #python #scientific-computing #cheatsheet

Things I can never remember when using Matplotlib.  There are many, though these seem to come up frequently.

# Twin Axes

```python
ax_h_twin = ax_h.twinx()
# plot on ax_h_twin

ax_h_twin.set_ylabel( "second axes label" )

# skip this if you don't need the label color to match the plot color.
ax_h_twin.yaxis.label.set_color( color )
```

