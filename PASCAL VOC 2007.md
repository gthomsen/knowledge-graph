Tags: #ml-dataset #computer-vision 

3rd year of the PASCAL VOC Challenges with increased (to 20) class counts and a simple class hierarchy.

| Source | Date | Label Types | Samples (Train/Validation/Test/Testval) | Classes | Commercial Use? |
| --- | --- | --- | --- | --- | --- |
| [Website](http://host.robots.ox.ac.uk/pascal/VOC/voc2007/) | 2007 | Classes, bounding boxes, difficulty flag | 14,974 (2,501/2,510/4,952/5,011) | 20 | [Flickr Terms of Use](http://www.flickr.com/terms.gne?legacy=1) |

# Details
 [Development Kit PDF](http://host.robots.ox.ac.uk/pascal/VOC/voc2007/devkit_doc_07-Jun-2007.pdf) describing the challenges, data, labels, and submission process.  [Training/validation data](http://host.robots.ox.ac.uk/pascal/VOC/voc2007/VOCtrainval_06-Nov-2007.tar) is ~450 MB, [test data](http://host.robots.ox.ac.uk/pascal/VOC/voc2007/VOCtest_06-Nov-2007.tar) is ~430 MB.  Metadata are provided in HDF5 format.
 
## Samples
Color images in JPEG format.  Presumably sourced from Flickr given the licensing.

## Classes
Two-level hierarchy of simple classes:
- Person
    - Person
- Animal
    - Bird
    - Cat
    - Cow
    - Dog
    - Horse
    - Sheep
- Vehicle
    - Aeroplane
    - Bicycle
    - Boat
    - Bus
    - Car
    - Motorbike
    - Train
- Indoor
    - Bottle
    - Chair
    - Dining table
    - Potted plant
    - Sofa
    - TV/monitor
