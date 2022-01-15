Tags: #ml-dataset #computer-vision 

Long-tailed dataset on natural images from Fine Grained Visual Classification 4 (FGVC^4).  For image classification and object detection with long-tailed class distributions.

| Name |Source | Date | Label Types | Samples (Train/Validation) | Classes | Commercial Use? |
| --- | --- | --- | --- | --- | --- | --- |
| iNaturalist 2017 | [Paper](https://openaccess.thecvf.com/content_cvpr_2018/papers/Van_Horn_The_INaturalist_Species_CVPR_2018_paper.pdf) | 2017 | Classes, 2D bounding boxes | 675,170 (579,184/95,986) labels.  544,900 (496,164/48,736) bounding boxes. | 5,089 categories with 13 super-categories | No |

# Details
Collected as part of a collaboration between Caltech, Cornell Tech and Google.

[Github page with data](https://github.com/visipedia/inat_comp/tree/master/2017)

# Samples
675,170 training and validation samples.  Potentially multiple labels per sample.  
544,900 bounding boxes, though unclear on which images.

# Classes
5,089 categories with 13 super-categories including plants, insects, birds, and mammals.  Long-tail distribution with 196,613 plant images in 2,101 plant-related categories, as well as a protozoa super category with 381 images in 4 sub-categories.

Details on the [Github page](https://github.com/visipedia/inat_comp/tree/master/2017#details).  ["The iNaturalist Species Classification and Detection Dataset"](https://arxiv.org/abs/1707.06642) Table 3 has explicit counts for labels in training and validation.

Bounding boxes are available for super-classes except the following:
- Plants
- Fungi
- Chromista
- Protozoa