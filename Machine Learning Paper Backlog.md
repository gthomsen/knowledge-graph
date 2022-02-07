Tags: #todo #machine-learning #paper-review 

List of papers I'll never get a chance to read.

# Self-Supervised Learning
- ["Scaling and Benchmarking Self-Supervised Visual Representation Learning"](https://arxiv.org/abs/1905.01235) by Goyal, Mahajan, Gupta, and Misra (2019).  Attempts to set a standard benchmark for evaluating self-supervised techniques.
- ["BYOL for Audio: Self-Supervised Learning for General-Purpose Audio Representation"](https://arxiv.org/abs/2103.06695v2) by Niizumi, Takeuchi, Ohishi, Harada, and Kashino (2021).  Applies BYOL to audio by using mel-spectrograms.
- ["Vision Transformer for Small-Size Datasets"](https://arxiv.org/abs/2112.13492v1) by Lee, Lee, and Song (2021).  Augmentation to allow small datasets to benefit from Transformers.  Uses [[ImageNet Dataset|Tiny ImageNet]].
- ["Self-supervised Learning from 100 Million Medical Images"](https://arxiv.org/abs/2201.01283v1). Domain-specific augmentations for self-supervised learning on medical X-rays in 2D and 3D.
- ["PointContrast: Unsupervised Pre-training for 3D Point Cloud Understanding"](https://arxiv.org/pdf/2007.10985.pdf) by Xie, Gu, Guo, Qi, Guibas, and Litany (2020). Applying unsupervised techniques to non-Imagenet dataset.  This may be the model referenced in Ishan Misra's podcast circuit in the summer of 2021.
- ["Training data-efficient image transformers & distillation through attention"](https://arxiv.org/abs/2012.12877v2) by Touvron, Cord, Douze, Massa, Sablayrolles, and Jegou (2021). Data-efficient image Transformers (DeiT) focuses on building models on "small" datasets ([[ImageNet Dataset|ImageNet]]) in several days on a single system.

# Representations
- ["Do Vision Transformers See Like Convolutional Neural Networks?"](https://arxiv.org/abs/2108.08810v1) by Raghu, Unterthiner, Kornblinth, Zhang, and Dosovitskiy (2021).  Applies Kornblinth's activation map technique to assess layer performance (relative to capacity).
- ["Why Do Better Loss Functions Lead to Less Transferable Features"](https://arxiv.org/abs/2010.16402) by Kornblith, Chen, Lee, and Norouzi (2020)

# Activations
- ["Implicit Neural Representations with Periodic Activation Functions"](https://arxiv.org/abs/2006.09661) by Sitzmann and Martel (2020). SIREN activation function that is able to capture 2nd derivatives of images better than sigmoid- or ReLU-based activations.  [Additional images](https://www.vincentsitzmann.com/siren/).

# Medical
- ["Is it Time to Replace CNNs with Transformers for Medical Images"](https://arxiv.org/abs/2108.09038v1) by Matsoukas, Haslum, Soderberg, and Smith (2021).  Applying data-hungry transformers to a data-starved domain.  References several medical image benchmark datasets.

# Engineering
- ["Debugging the Internals of Convolutional Networks"](https://ai.facebook.com/research/publications/debugging-the-internals-of-convolutional-networks/) from Facebook (2021).  Works through identifying artifacts in learned convolutional filters.
- ["Bag of Tricks for Image Classification for Convolutional Neural Networks"](https://arxiv.org/abs/1812.01187) by He, Zhang, Zhang, Zhang, Xie, and Li (2018). Collection of techniques to improve convolutional networks that aren't specific to a particular architecture or dataset.  Used by YOLOv4.

# Big Models
- ["Switch Transformers: Scaling to Trillion Parameter Models with Simple and Efficient Sparsity"](https://arxiv.org/abs/2101.03961) by Fedus, Zoph, and Shazeer (2021). 1e12 parameter model with constant computational cost through mixture of experts approach.

# Computer Vision
- ["Swin Transformer V2: Scaling Up Capacity and Resolution"](https://arxiv.org/abs/2111.09883v1) by Liu, Hu, Yao, Xie, Wei, Ning, Cao, Zhang, Dong, Wei, and Guo (2021).  Techniques to bootstrap high resolution models from lower resolution images, and train big models on regular GPUs.
- ["A Survey of Visual Transformers"](https://arxiv.org/abs/2111.06091) by Liu, Zhang, Wang, Hou, and Yuan (2021)
- ["How to train your ViT? Data, Augmentation, and Regularlization in Vision Transformers"](https://arxiv.org/abs/2106.10270) by Steiner et al (2021).  Explores the amount of performance gain from data augmentation from the standpoint of training with smaller datasets.

## Object Detection
- ["Learning non-maximum suppression"](https://arxiv.org/abs/1705.02950) by Hosang, Benenson, and Schiele (2017). Trainable non-maximal suppression (NMS) using only boxes and scores.  Replaces hand-crafted non-trainable methods.
- ["End-to-End Object Detection with Adaptive Clustering Transformer"](https://arxiv.org/abs/2011.09315) by Zheng et al (2021).  Presents DETR to do object detection with Transformers.
- ["UP-DETR: Unsupervised Pre-training for Object Detection with Transformers"](https://arxiv.org/abs/2011.09094) by Dai et al (2021).  Unsupervised training and supervised distillation using transformers for object detection.

## Segmentation
- ["Simple Copy-Paste is a Strong Data Augmentation Method for Instance Segmentation"](https://arxiv.org/abs/2012.07177v2) by Google Brain, Berkeley, and Cornell (2021).

# Miscellaneous
- ["The Hardware Lottery"](https://arxiv.org/abs/2009.06489v1) by Sara Hooker (2020).  Discussion about how hardware selection has prevented progress because otherwise successful ideas didn't map onto the existing hardware.
- ["Deep Learning Interviews"](https://arxiv.org/ftp/arxiv/papers/2201/2201.00650.pdf) by Shlomo Kashani (2020).
- ["Large Batch Training of Convolutional Networks"](https://arxiv.org/abs/1708.03888v3) by You (2017).  Presents layer-wise adaptive rate scaling (LARS).