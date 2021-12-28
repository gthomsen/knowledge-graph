Tags: #python #cheatsheet

Dumping ground for basic concepts in `python-pptx`.  Distilled from the [documentation](https://python-pptx.readthedocs.io/en/latest/index.html).

# Sizes are in EMUs
All sizes are in English Metric Units (EMUs) though this is hidden by the `pptx.util` module. Its methods allow specification in other units and handles conversion to EMUs.  Useful units are:
- `pptx.util.Inches()` - inches
- `pptx.util.Cm()` - centimeters
- `pptx.util.Pt()` - points

# Object Hierarchy
Presentations -> Slides -> Shapes

# Pictures
Picture attributes:
- `.crop`: value in [0, 1] specifying the crop percentage from the respective edge
- `.height`, `.width`: Size specified as an integral number of EMUs
- `.left`, `.top`: Position to upper-left corner in EMUs
- `.image`: [[#Images|Image]] object
- `.line`: LineFormat object representing the border

# Images
Created via the `.shapes.add_picture()` method.

Image attributes:
- `.blob`: Bytestream containing the image
- `.content_type`: MIME type
- `.ext`: Canonical file extension
- `.dpi`: Tuple containing the (horizontal, vertical) dots per inch
- `.filename`: Path where the image came from, `None` if not backed by disk
- `.size`: Tuple containing (width, height) in EMUs

# Shapes
Shape attributes:
- `.line`: LineFormat object representing the border
- `.text`: Text for the shape.  Newlines are paragraph breaks, vertical tabs (`\v`) are line breaks.
- `.text_frame`: TextFrame for `.text`.  Used for formatting the contents of `.text`.

