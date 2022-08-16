Tags: #ml-dataset #computer-vision 

8th (and final) year of the PASCAL VOC Challenges.

| Source | Date | Label Types | Samples (Train/Validation/Test/Testval) | Classes | Commercial Use? |
| --- | --- | --- | --- | --- | --- |
| [Website](http://host.robots.ox.ac.uk/pascal/VOC/voc2012/) | 2012 | Classes, bounding boxes, difficulty flag | ? (?/?/?/?) | 20 | [Flickr Terms of Use](http://www.flickr.com/terms.gne?legacy=1) |

# Details
 [Development Kit PDF](http://host.robots.ox.ac.uk/pascal/VOC/voc2012/devkit_doc.pdf) describing the challenges, data, labels, and submission process.  [Training/validation data](http://host.robots.ox.ac.uk/pascal/VOC/voc2012/VOCtrainval_11-May-2012.tar) is ~2 GB, [test data](http://host.robots.ox.ac.uk:8080/) may be available in aggregate, but requires an account.  Metadata are provided in HDF5 format.
 
## Samples
Color images in JPEG format.  Presumably sourced from Flickr given the licensing.

## Classes
Two-level hierarchy of simple classes (same as [[PASCAL VOC 2007]]):
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
