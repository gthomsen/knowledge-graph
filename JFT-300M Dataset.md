Tags: #ml-dataset #computer-vision 

Internal Google dataset for image classification.

| Name |Source | Date | Label Types | Samples (Train/Test) | Classes | Commercial Use? |
| --- | --- | --- | --- | --- | --- | --- |
| JFT-300M | [ICCV 2017 Paper](https://arxiv.org/abs/1707.02968v2) | 2017 | Classes | 300M (?/?) | 18,291 | No |

# Details
Introduced in ["Revisiting Unreasonable Effectiveness of Data in Deep Learning Era"](https://arxiv.org/abs/1707.02968v2) by Sun et al (2017).

## Labels
375M labels, so each image has on average 1.26 labels.

## Classes
Varying levels of class hierarchies, up to 12 deep, with a maximum branch width of 2,876. Of the 18,291 classes, 1,165 are animals and 5,720 are vehicles.  941 labels have a direct correspondence to classes in [[ImageNet Dataset|ImageNet]].

Lots of long tail distributions - more than 3,000 categories (15%) with less than 100 images each, and roughly 2,000 categories (10%) with fewer than 20 images per category.
