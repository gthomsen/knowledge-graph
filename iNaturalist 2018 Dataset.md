Tags: #ml-dataset #computer-vision 

Long-tailed dataset on natural images from Fine Grained Visual Classification 5 (FGVC^5).  For image classification with long-tailed class distributions.  Not a superset of [[iNaturalist 2017 Dataset]] and does not support object detection.  Has a separate test dataset.

| Name |Source | Date | Label Types | Samples (Train/Validation/Test) | Classes | Commercial Use? |
| --- | --- | --- | --- | --- | --- | --- |
| iNaturalist 2018 | Paper | 2018 | 461,939 (437,512/24,426/149,394) | 8,142 | No |

# Details
Collected as part of a collaboration between Caltech, Cornell Tech and Google.

[Github page with data](https://github.com/visipedia/inat_comp/tree/master/2018).

# Samples
461,939 training and validation images. 149,394 test images.

# Classes
$\ge 8000$ classes of plants, animals, and fungi.  Has a long-tail distribution with 5,000-6,000 classes with 20 images or less.

Labels are more detailed with taxonomy information (kingdom, phylum, class, order, family, and genus) than in iNaturalist 2017.

![iNaturalist 2018 Training and Validation Distribution](https://raw.githubusercontent.com/visipedia/inat_comp/master/2018/assets/train_val_distribution.png)