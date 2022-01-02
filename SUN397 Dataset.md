Tags: #ml-dataset #computer-vision 

Subset of the Scene UNderstanding (SUN) database.  All scene categories have at least 100 images.

| Source | Date | Label Types | Samples (Train/Test) | Classes | Commercial Use? |
| --- | --- | --- | --- | --- | --- |
| [Paper](https://vision.princeton.edu/projects/2010/SUN/paper.pdf), [Homepage](https://vision.princeton.edu/projects/2010/SUN/), [Dataset](http://vision.princeton.edu/projects/2010/SUN/SUN397.tar.gz), [Code](https://vision.princeton.edu/projects/2010/SUN/source_code/) | Labels, instance segmentation masks | 108,754 (?/?) | 397 | Unknown|

# Details
Aude Olivia was involved.

## Samples
Dataset is 39 GB compressed.  [Original URLs](https://vision.princeton.edu/projects/2010/SUN/urls/) for scenes in the database.

## Labels
Segmentation masks are per-instance.

## Classes
The classes used are in an [zipped Excel spreadsheet](https://vision.princeton.edu/projects/2010/SUN/hierarchy_three_levels.zip).  All classes have at least 100 images in them.

### Scenes
Scene categories are arranged in a 3-level hierarchy with 3 top-level  superordinate categories, 15 basic categories, and 908 scene categories.  The database can be interactively explored [here](https://vision.princeton.edu/projects/2010/SUN/hierarchy/).

Superordinate categories:
1. Indoor
2. Outdoor natural
3. Outdoor man-made

Indoor categories:
1. Shopping and dining
2. Workplace
3. Home or hotel
4. Transportation
5. Sports and leisure
6. Cultural

Natural outdoor categories:
7. Water, ice, snow
8. Mountains, hills, desert, sky
9. Forest, field, jungle
10. Man-made elements

Man-made outdoor categories:
11. Transportation
12. Cultural or historical building/place
13. Sports fields, parks, leisure spaces
14. Industrial and constructions
15. Houses, cabins, gardens, and farms
16. Commercial buildings, shops, markets, cities, and towns

### Objects
Segmented objects come from 3,819 classes (it appears that the [ADE20K dataset](https://groups.csail.mit.edu/vision/datasets/ADE20K/) shares the classes).  These differ from PASCAL VOC.