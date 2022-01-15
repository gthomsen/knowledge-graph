Tags: #ml-dataset #computer-vision 

Personal holidays photos collected by INRIA researchers.  Artificially distorted images for clutter purposes.  SIFT features available.

| Name |Source | Date | Label Types | Samples (Train/Validation) | Classes | Commercial Use? |
| --- | --- | --- | --- | --- | --- | --- |
| INRIA Holidays | [Paper](https://hal.inria.fr/inria-00548651/document/) | 2008 | Visual descriptors | 1,491 (500/991) | ? | ? |
| INRIA Copydays | N/A | 2008 | None? | 229+ | None | ? |

# Samples
High resolution (1024x768) images for image descriptor-based techniques.

## Holidays
1,491 images.  500 query images and 991 associated images across all queries.  Large variety of scene types - natural, manmade, water, fire effects, etc.

Each image has SIFT descriptors, 128D, with a total of 4,455,091 descriptors for the dataset.

## Copydays

Distorted versions of the [[#Holidays]] data.  Some images have JPEG artifacts induced by changing the quality factors (down to Q=5), some are cropped (leaving as little as 20% of the image), and some are manipulated (print and scanned, blurred, painted over, etc).

Intended to supplement the Holidays dataset.