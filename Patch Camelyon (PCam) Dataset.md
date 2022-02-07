Tags: #ml-dataset #computer-vision 

Color imagery of lymph node cross sections to detect metastastic tissues.  From Max Welling's research lab.

| Source | Date | Label Types | Samples (Train/Validation/Test) | Classes | Commercial Use? |
| --- | --- | --- | --- | --- | --- |
| [Paper](https://arxiv.org/abs/1806.03962), [Data](https://github.com/basveeling/pcam) | 2018 | Binary labels | 327,680 (262,144/32,768/32,768) | 2 | ? |

# Details
96x96 color images from histopathologic scans of lymph node sections.  Classified as metastatic if cancerous tissue is in the center 32x32 pixels, normal otherwise.

![Patch Camelyon Exemplar Montage](https://storage.googleapis.com/tfds-data/visualization/fig/patch_camelyon-2.0.0.png)

## Samples
Centered labels were made with the intent that convolutional architectures did not have to zero pad the input, which would be consistent with application to a whole-slide image.

Pixel resolution of 0.243 $\mu$m and then downsampled by 10x.

Train, validation, and test splits (75%/12.5%/12.5%) are provided for consistent evaluation.

## Benchmark
Performance evaluation takes into account the rotational and mirror symmetries to explore real-world performance where patch orientation is one of 8 combinations.  This is inline with the group equivariance work that Welling's group focused on at the time.