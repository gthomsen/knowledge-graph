Tags: #machine-learning #computer-vision #paper-review #unfinished 

["An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale"](https://arxiv.org/abs/2010.11929v2) by Dosovitskiy et al (2021).  Work done by Google Brain to apply the [[Transformer Architecture|Transformer architecture]] to computer vision tasks.

Unanswered questions:
- When would you not want to use a CLS token?

# Position Encoding
Input patch size is fixed by the architecture, though the input image size is not explicitly.  The input image size can change after training so long as the position encodings used are interpolated consistently.  So long as the feature sizes have the same distribution between small training images and larger production images, the only degradation is the FLOPS required to process more patches.

# Google Research Implementation
Things to note:
- [Implemented in JAX](https://github.com/google-research/vision_transformer) rather than TensorFlow or PyTorch.
- [ResNet can be used as the embedding front end](https://github.com/google-research/vision_transformer/blob/3f3b50d3490f8b2f46f084a14683407b41f5c5a7/vit_jax/models.py#L228).
- [Class token is initialized to zero](https://github.com/google-research/vision_transformer/blob/3f3b50d3490f8b2f46f084a14683407b41f5c5a7/vit_jax/models.py#L274).

# Unofficial PyTorch Implementation
[tczhangzhi/VisionTransformer-Pytorch](https://github.com/tczhangzhi/VisionTransformer-Pytorch) is licensed under Apache 2.0.

# Official PyTorch Implementation
Has a [understandable implementation](https://pytorch.org/vision/main/_modules/torchvision/models/vision_transformer.html) that makes it clear the mapping between batches, patches, and inputs.  A batch of input images its turned into a batch of sequences of embeddings.  In the PyTorch implementation, embeddings are generated using `nn.Conv2D()` though in other implementations (e.g. [[#Google Research Implementation|Google's]]) you have the option of using a full up ResNet-50 backbone.

Relevant code (with my comments):

```python
Class VisionTransformer( nn.Module ):
    def __init__( ... ):
        ...

        self.image_size = image_size   # assumes a square image.
        self.patch_size = patch_size   # assumes a square patch.
        self.hidden_dim = hidden_dim   # embedding size.

        ...

        # computes embeddings by a single 2D convolution that is
        # sized pxp (for p=patch_size) with stride of p so that
        # each embedding is computed on an adjacent, non-overlapped
        # patches.
        #
        # computes hidden_dim-many outputs (the embedding for each
        # patch) with an output size of:
        #
        #   (width / patch_size) x (height / patch_size).
        #
        self.conv_projector = nn.Conv2D( input_channels,
                                         hidden_dim,
                                         kernel_size=patch_size,
                                         stride=patch_size )

        # compute the number of patches in the image.
        seq_length = (image_size // patch_size)**2

        ...

    def _process_input( self, x ):

        # get the shapes of the data.
        n, c, h, w = x.shape
        p          = self.patch_size

        # number of patches in each dimension.
        (n_h, n_w) = (h // p), (w // p)

        # use a Conv2D() to get embeddings as a function of patch.
        # (n, c, h, w) -> (n, hidden_dim, n_h, n_w)
        x = self.conv_projector( x )

        # collapse the patch grid into a sequence of patches so the
        # permutation below is more efficient.
        # (n, hidden_dim, n_h, n_w) -> (n, hidden_dim, (n_h * n_w))
        x = x.reshape( n, self.hidden_dim, n_h * n_w )

        # the Encoder expects (batches, sequences, embedding).
        # (n, hidden_dim, (n_h * n_w)) -> (n, (n_h * n_w), hidden_dim)
        x = x.permute( 0, 2, 1 )

        return x

    def forward( self, x ):
        x = self._process_input( x )

        # XXX: broadcast the CLS token and add to the embeddings
        # XXX: pass the embeddings into the Encoder
```

All input images **MUST** be the same size so that the sequence length in the encoder can be fixed.