Tags: #ml-dataset #computer-vision 

Improvement over the Densely-Annotated VIdeo Segmentation (DAVIS) 2016 dataset with 3x the samples/frames and also having finer-grained classes.

| Name |Source | Date | Label Types | Samples (Train/Validation) | Classes | Commercial Use? |
| --- | --- | --- | --- | --- | --- | --- |
| DAVIS17 | [Paper](https://arxiv.org/abs/1704.00675) | 2017 | Instance segmentation masks | ? | ? | ? |

# Details
Second dataset, of four, in the [DAVIS collection](https://davischallenge.org/).  Despite the high resolution samples, the original competition was performed against versions downsampled to 480p.

# Samples
From ["The 2017 DAVIS Challenge on Video Object Segmentation"](https://arxiv.org/abs/1704.00675) Table 1:

| Category | Number Sequences | Number Frames | Mean Number Frames per Sequence | Number Objects | Mean Number Objects Per Sequence |
| --- | --- | --- | --- | --- | --- |
| Training | 60 | 4,219 | 70.3 | 138 | 2.30 |
| Validation | 30 | 2,023 | 67.4 | 59 | 1.97 |
| Test (Dev) | 30 | 2,037 | 67.9 | 89 | 2.97 |
| Test (Challenge) | 30 | 2,180 | 72.7 | 90 | 3.0 |

Videos are mostly 4K resolution (3840x2160) though videos carried over from DAVIS16 include 1440p, 1080p, and 720p.

# Classes
Unknown which classes are present.