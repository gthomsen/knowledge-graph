Tags: #ml-dataset #computer-vision 

Meta-dataset from Google Brain that aggregates 19 datasets (from natural, specialized, and structured categories) and presents new metrics on evaluation model performance.  Aims to evaluate learned representations and their ability to transfer/generalize.

| Source | Date | Label Types | Samples (Train/Validate/Test) | Classes | Commercial Use? |
| --- | --- | --- | --- | --- | --- |
| [Paper](https://arxiv.org/abs/1910.04867) | 2020 | Varied | Varied | Varied | Varied | Partial? |

# Details
From [[A Large-scale Study of Representation Learning with the Visual Task Adaptation Benchmark|"A Large-scale Study of Representation Learning with the Visual Task Adaptation Benchmark"]] by Zhai, Puigcerver, and Kolesnikov (2020).

# Tasks
19 tasks are grouped into three sets:
1. Natural: Natural images collected with standard cameras
2. Specialized: Images collected with specialized instruments
3. Structured: Data that represents the structure of a scene (e.g. point cloud)

Derived from the Appendix A's Table 2:

| Category | Dataset | Training Samples | Classes |
| --- | --- | --- | --- |
| Natural | [[Caltech-101 Dataset|Caltech101]] | 3,060 | 102 |
| Natural | [[CIFAR-100 Dataset|CIFAR-100]] | 50,000 | 100 |
| Natural | [[Describable Textures Dataset (DTD)|DTD]] | 3,760 | 47 |
| Natural | [[Flowers 101 Dataset|Flowers102]] | 2,040 | 102 |
| Natural | [[Oxford-IIIT-Pet Dataset|Pets]] | 3,680 | 37 |
| Natural | [[SUN397 Dataset|SUN397]] | 87,003 | 397 |
| Natural | SVHN | 73,257 | 10 |
| Specialized | [[EuroSAT Dataset|EuroSAT]] | 21,600 | 10 |
| Specialized | [[Resisc45 Dataset|Resisc45]] | 25,200 | 45 |
| Specialized | Patch Camelyon | 294,912 | 2 |
| Specialized | Retinopathy | 46,032 | 5 |
| Structured | Clevr/count | 70,000 | 8 |
| Structured | Clevr/distance | 70,000 | 6 |
| Structured | dSprites/location | 663,552 | 16 |
| Structured | dSprites/orientation | 663,552 | 16 |
| Structured | SmallNORB/azimuth | 36,450 | 18 |
| Structured | SmallNORB/elevation | 36,450 | 9 |
| Structured | DMLab | 88,178 | 6 |
| Structured | KITTI/distance | 5,711 | 4 |


