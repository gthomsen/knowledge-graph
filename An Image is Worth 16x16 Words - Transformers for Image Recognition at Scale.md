Tags: #machine-learning #computer-vision #paper-review #unfinished 

["An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale"](https://arxiv.org/abs/2010.11929v2) by Dosovitskiy et al (2021).  Work done by Google Brain to apply the [[Transformer Architecture|Transformer architecture]] to computer vision tasks.

# Position Encoding
Input patch size is fixed by the architecture, though the input image size is not explicitly.  The input image size can change after training so long as the position encodings used are interpolated consistently.  So long as the feature sizes have the same distribution between small training images and larger production images, the only degradation is the FLOPS required to process more patches.