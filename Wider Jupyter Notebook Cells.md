Tags: #scientific-computing #python #jupyter 
By default Jupyter Notebook cells have a fixed width and do not use all available window real estate.  The following code can be run within a Notebook to update its behavior:

```python
from IPython.display import display, HTML

display( HTML( data="""
<style>
    div#notebook-container { width: 95%; }
    div#menubar-container { width: 65%; }
    div#maintoolbar-container { width: 99%; }
</style>
""" ) )
```

A permanent modification to all Notebooks via a user's custom CSS can be made by creating `${HOME}/.jupyter/custom/custom.css` with the following:
```css
.container {
    width: 99% !important;
}   

div.cell.selected {
    border-left-width: 1px !important;	
}

div.output_scroll {
    resize: vertical !important;
}
```

Jupyter must be restarted when using a custom CSS as restarting a kernel is not sufficient.

Derived from this [Github gist](https://gist.github.com/paulochf/f6c9ed0b39f85dd85270).