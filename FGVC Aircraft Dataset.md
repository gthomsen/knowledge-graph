Tags: #ml-dataset #computer-vision

Fine-grained visual classification (FGVC) of aircraft.

| Source | Date | Label Types | Samples (Train/Test) | Classes | Commercial Use? |
| --- | --- | --- | --- | --- | --- |
| [arXiv paper](https://arxiv.org/abs/1306.5151v1) | 2013 | Boxes, classes| 10,200 (6,667/3,333)| 102 | No |

# Details
## Samples
Each sample has a 20-pixel high copyright banner along the top.  These must be cropped prior to training.

## Classes
Aircraft models have a 4-level hierarchy of labels:
1. Manufacturer (e.g. Boeing)
2. Family (e.g. Boeing 737)
3. Variant (e.g. Boeing 737-700)
4. Model (e.g. Boeing 737-76J)

Typically only the first three hierarchies are used and the Model label is ignored since models from the same variant typically differ in non-visual ways.