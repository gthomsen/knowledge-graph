Tags: #todo 

Junk drawer of things to look at when I have infinite free time.

# Programming
- Google's Abseil C++ library ([Github](https://github.com/abseil/abseil-cpp))
- Facebook's Folly C++ library ([Github](https://github.com/facebook/folly)).  Built on top of Boost.

## Tooling
- Facebook's [`drgn` kernel debugger](https://developers.facebook.com/blog/post/2021/12/09/drgn-how-linux-kernel-team-meta-debugs-kernel-scale/).  Python environment that has access to the kernel's symbols.
- Container building anti-patterns [blog post](https://jpetazzo.github.io/2021/11/30/docker-build-container-images-antipatterns/).
- Facebook's [Pysa](https://engineering.fb.com/2020/08/07/security/pysa/).  Python static analysis tool.
- [Deep dive](https://blog.palantir.com/optimizing-gits-merge-machinery-1-127ceb0ef2a1) on optimizing how `git merge` works.  [Part 2](https://blog.palantir.com/optimizing-gits-merge-machinery-2-d81391b97878) and [part 3](https://blog.palantir.com/optimizing-gits-merge-machinery-3-2dc7c7436978).

# Emacs
- [`Wilfred/deadgrep`](https://github.com/Wilfred/deadgrep) - fast search via `ripgrep`.

# Scientific Computing
- [High-resolution ocean simulation with Jax](https://dionhaefner.github.io/2021/12/supercharged-high-resolution-ocean-simulation-with-jax/). Covers porting from original Fortran code and benchmarking against multiple alternative implementations (NumPy, JAX + MPI, etc).
- [StackOverflow post](https://stackoverflow.com/questions/55222312/do-most-compilers-optimize-matmultransposea-b) on compilers optimizing `matmul( transpose( A ), B )`. Good analysis on measuring performance of `ifort` and `gfortran`'s builtins vs using BLAS to compute matrix multiplications.
- [Interactive visualization](https://static.laszlokorte.de/fourier/) showing Fourier transforms.
- Building containers for Exascale:
    - ["Minimizing privilege for building HPC containers"](https://arxiv.org/pdf/2104.07508.pdf) by Priedhorsky and Reid (2021)
- [StackOverflow question](https://stackoverflow.com/questions/54039225/how-does-numpy-move-data-when-transpose-a-matrix) that explores data views and movement under transposition.
- [Umpire](https://github.com/LLNL/Umpire) is a memory allocator library from LLNL.  Supports NUMA and GPUs. ["Umpire: Application-focused management and coordination of complex hierarchy memory"](https://ieeexplore.ieee.org/document/8907404).

## Tensor Contractions
- Facebook's [Tensor Comprehensions library](https://ai.facebook.com/tools/tensorcomprehensions) generates GPU code from high-level mathematical descriptions.  Older library (from 2017) but is useful for understanding concepts/design.

## Floating Point Arithmetic
- [Numerical Computing with IEEE Floating Point Arithmetic](https://cs.nyu.edu/~overton/book/index.html) - highly reviewed book on floating point from 2001.
- [Herbie](https://herbie.uwplse.org/doc/latest/faq.html).  Transforms floating point expressions into more accurate forms.
- [Seminar on reduced precision error analysis for ML.](https://indico.cern.ch/event/1012375/attachments/2219334/3757933/VolkovaLauter_DNNAnalysis_seminar.pdf) [Video of the event](https://indico.cern.ch/event/1012375/attachments/2219334/3757934/zoom_0.mp4).

# Mathematics
- [11 proofs of the Gaussian integral](https://kconrad.math.uconn.edu/blurbs/analysis/gaussianintegral.pdf).  From [Hacker News](https://news.ycombinator.com/item?id=28507114).
- [sepandhaghighi/samila](https://github.com/sepandhaghighi/samila) - Generative art in Python

# Performance Tuning
- ["Roofline: An Insightful Visual Performance Model for Floating-Point Programs and Multicore Architectures"](https://people.eecs.berkeley.edu/~kubitron/cs252/handouts/papers/RooflineVyNoYellow.pdf) by Williams, Waterman, and Patterson (2008).
- ["LibShalom: Optimizing Small and Irregular-shaped Matrix Multiplications on ARMv8 Multi-Core"](http://jianbinfang.github.io/files/2021-06-22-sc.pdf) by Yang et al (2021). ARM-specific BLAS library tuned for small matrices, similar to BLASFEO, though is designed to exploit multi-core.

# Networking
- Youtube video ["Running BGP in Data Centers at Scale"](https://www.usenix.org/conference/nsdi21/presentation/abhashkumar) covering Facebook's use of BGP in the datacenter. 

# Cloud Instances
- [Vast.ai](https://vast.ai/console/create/) for spot instances on people's systems.

# Blogs
- Simon Willison's [TIL Github](https://github.com/simonw/til).  Interesting technology snippets.  Good model for consolidating information.
- [Caius Theory](https://caiustheory.com/).  Sparse collection of deep dive posts.
- [Jethro's Brain Dump](https://braindump.jethro.dev/posts/).  Knowledge graph of the guy who created [`org-roam`](https://www.orgroam.com/).
- [Alexis Rondeau's Digital Garden](https://publish.obsidian.md/alexisrondeau/Welcome+to+my+digital+garden).  Heavy user of Obsidian.
- ["Fast CSV processing with SIMD"](https://nullprogram.com/blog/2021/12/04/) from [Chris Wellons](https://nullprogram.com/) (null program).  Deep dive on optimizing CSV parsing with vector instructions.
- ["How Not To Sort By Average Rating"](https://www.evanmiller.org/how-not-to-sort-by-average-rating.html) by [Evan Miller](https://www.evanmiller.org/). Math-heavy explanation on computing a relevance score (using something from Edwin Wilson!) for sorting results.
- ["How to Train Really Large Models on Many GPUs?"](https://lilianweng.github.io/lil-log/2021/09/24/train-large-neural-networks.html) by [Lillian Weng](https://lilianweng.github.io/lil-log/). ML person at OpenAI who can coney things clearly and deeply.
- [Inigo Quilez's tutorials on computer graphics](https://iquilezles.org/www/index.htm).  Ray tracing through signed distance functions (SDF) and lots of examples on ShaderToy.
    - [Zoo of primitives](https://www.iquilezles.org/www/articles/distfunctions/distfunctions.htm) implemented as SDF shaders.
- Hacker News discussion on [good engineering blogs](https://news.ycombinator.com/item?id=29237308).
- [John McCalpin "Dr. Bandwidth"'s blog](https://sites.utexas.edu/jdm4372/).  Deep dives on processor architectures with a TACC-centric focus.
- [Paul Bridger](https://paulbridger.com/) is a ML engineer with several deep dive posts on optimizing computer vision models for inferencing.

# Productivity
- HackerNews discussion on [hiring personal assistants](https://news.ycombinator.com/item?id=29336234).

## Note Taking
- [QuickDown](https://github.com/akaalias/quickdown) for MacOS.  Global hotkey to take a Markdown note.  Can complement [[Obsidian]].
- [Alexis Rondeau's Github](https://github.com/akaalias).  Lots of [[Obsidian]]-related tools.

# Machine Learning
- DARPA's [Adversarial Robustness Toolbox (ART)](https://github.com/Trusted-AI/adversarial-robustness-toolbox/wiki/ART-Architecture-and-Roadmap). Attacks, defenses, and metrics for adversarial attacks on ML.  [Announcement](https://www.darpa.mil/news-events/2021-12-21).
- Evaluate the personal plan from [Weights & Biases](https://wandb.ai/site/pricing#compare-plans) to see how it does for tracking experiments and hyperparameters.
- Understand what [spaCy](https://spacy.io/) provides for NLP applications. Presumably provides models and APIs that would otherwise be built by hand for common tasks.  [Simple 4 chapter course](https://course.spacy.io/en/) with it.
- [NeurIPS visualization blog post](https://neuripsav.vizhub.ai/blog/) clusters accepted papers.  Can filter by time and by clusters to review paper titles.  Does not have links.
- Deep dive on [JAX's Autodidax](https://jax.readthedocs.io/en/latest/autodidax.html).
- Animated cartoons showing how [attention is used in transformers](https://towardsdatascience.com/illustrated-self-attention-2d627e33b20a).
- [Blog post](https://www.machinecurve.com/index.php/2019/09/16/he-xavier-initialization-activation-functions-choose-wisely/) on He/Xavier initialization and their interactions with activation functions.
- [NumPy implementations of PyTorch's standard transforms](https://github.com/mlagunas/pytorch-nptransforms).  Unlicensed.
- PyTorch [memory format tutorial](https://github.com/pytorch/tutorials/blob/master/intermediate_source/memory_format_tutorial.py).  NHWC vs NCHW for accelerating kernels on Tensor Core-enabled GPUs.
- PyTorch [`torchinfo`](https://github.com/TylerYep/torchinfo) package.  Provides a model summary (parameter counts, estimated forward/backward pass sizes, etc).
- [Mixed precision training](https://developer.nvidia.com/blog/video-mixed-precision-techniques-tensor-cores-deep-learning/#part6) overview from NVIDIA.  Useful diagrams summarizing what happens.
- [NVIDIA documentation](https://docs.nvidia.com/deeplearning/performance/mixed-precision-training/index.html#tensorop) for mixed precision training.
- NVIDIA's DL Profiler [DLProf](https://docs.nvidia.com/deeplearning/frameworks/dlprof-user-guide/).  Useful for identify computational bottlenecks and whether they map onto Tensor Cores.
- [Hacker News discussion](https://news.ycombinator.com/item?id=28738141) on using cloud spot instances for training. spotML, Nimbo, and Metaflow are platforms to support this workflow.
- [Deep dive on GPUs and ML](https://timdettmers.com/2020/09/07/which-gpu-for-deep-learning/#Do_Not_Buy_These_GPUs).  Selecting GPUs for training and inferencing, focused on individual developers rather than large corporate clusters.
- [Gradient checkpointing with PyTorch](https://spell.ml/blog/gradient-checkpointing-pytorch-YGypLBAAACEAefHs) blog post.
- [L1 vs L2 regularization](https://explained.ai/regularization/L1vsL2.html).  Figures showing the difference.

## Activation Functions
- Swish and Hard Swish.  Hard Swish is designed to be mobile processor friendly.

## Datasets
- INat18, INat18
- VTAB - 19 tasks
- MNIST 8M
- DAVIS17
- Google Landmark V2 (GLDv2)
- Copydays
- YFCC100M

## Representations
- [Assessing quality of representations](https://wp.nyu.edu/cilvr/2020/09/24/representation-quality-and-the-complexity-of-learning/). Mentions the [Reprieve library](https://github.com/willwhitney/reprieve) for measuring quality - framework measures loss against a dataset and computes publication-ready plots.

## Frameworks
- [Catalyst](https://github.com/catalyst-team/catalyst) - end-to-end training/inferencing loop in PyTorch.  Provides reproducibility, DL best practices (SWA, AdamW, etc), workflow best practices (fp16, distributed training, DALI, etc).
- [DeepSpeed](https://github.com/microsoft/DeepSpeed) from Microsoft.  Distributed training framework for extremely large models.
- [FairScale](https://github.com/facebookresearch/fairscale) from Facebook.  Distributed training framework.
- Facebook's [VISSL library](https://vissl.ai/) for self-supervised learning. [Github](https://github.com/facebookresearch/vissl).  Contains implementations for SWaV, SimCLR, DINO, and Barlow Twins.

## Data Labeling
- [AlexeyAB/Yolo_mark](https://github.com/AlexeyAB/Yolo_mark) - tool for object detection labeling.  Minimal OpenCV application that (appears to) uses optical flow to adjust labels in successive frames.

## Object Detection
- [PyTorch implementation of YOLOv1](https://github.com/motokimura/yolo_v1_pytorch).  No license listed.
- [PyTorch implementation of YOLOv3](https://github.com/ultralytics/yolov3).  GPL licensed. 
- [PyTorch implementation of YOLOv4](https://github.com/Lornatang/YOLOv4-PyTorch).  Apache 2.0 licensed.
- [PyTorch implementation of YOLOv5](https://github.com/ultralytics/yolov5/).  GPL licensed.
- [dddzg/up-detr](https://github.com/dddzg/up-detr).  Apache 2.0 licensed.

### Speeding Up Inferencing
- [Sparsifying YOLOv5 on CPUs](https://neuralmagic.com/blog/benchmark-yolov5-on-cpus-with-deepsparse/).  Technical walkthrough quantizing and pruning the network, though misrepresents GPU benchmark (doesn't use Tensor Cores).  [Discussion on Hacker News](https://news.ycombinator.com/item?id=28484373) talks about cloud prices drastically favor CPUs ($10/month vs $1000/month).
- [Blog post](https://paulbridger.com/posts/video-analytics-pipeline-tuning/) on speeding up NVIDIA's SSD300 on GPUs using Python.  Works through using NSight Systems to identify bottlenecks.

## Reinforcement Learning
- 3 part series training an agent to play Dominion.  [Part 1](https://ianwdavis.com/dominion.html), [part 2](https://ianwdavis.com/dominion2.html), and [part 3](https://ianwdavis.com/dominion3.html).  [Github repository](https://github.com/iwd32900/dominion-ai).
- [TimDarcet/gym-azul](https://github.com/TimDarcet/gym-azul) gym for training agents to play Azul.

## Graph Neural Networks
- [ESE 514 - Graph Neural Networks](https://gnn.seas.upenn.edu/) course at University of Pennsylvania.

# Research Sources
- [All research streams](https://research.facebook.com/publications/are-large-scale-datasets-necessary-for-self-supervised-pre-training/?%2F) from Facebook.
- [Inter-experimental LHC Machine Learning Working Group](https://iml.web.cern.ch/meetings?page=0) monthly meetings are a good source of applying ML to sensor processing problems.  Mixtures of traditional machine learning and deep learning.