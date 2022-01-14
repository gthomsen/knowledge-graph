Tags: #paper-review #machine-learning #nlp 

["Attention is All You Need"](https://arxiv.org/abs/1706.03762) by Vaswani et al (2017) introduced the [[Transformer Architecture|Transformer architecture]] for NLP tasks, replacing recurrent network architectures (e.g. RNNs, LSTMs, and GRUs).

Reports [[Bilingual Evaluation Understudy (BLEU) Metric|BLEU]] of 28.4 for [[WMT 2014 Language Translation Dataset|WMT 2014]] English-to-German translation (4.5M sentences), and 41.8 for WMT 2014 English-to-French translation (36M sentences).  Scores are from supervised training since the source and target language sentences are available.

F1 score of 92.7.

Self-attention provides several key benefits:
- Removes distance limitations on positions' influence.  The first symbol can influence the last symbol (and all in between) regardless of sequence length.
- Attention heads are matrix multiplications and element-wise operations.  Very efficient to execute.
- All symbols in the sequence are processed simultaneously.

Symbol position is encoded as a sinusoidal embedding that is summed into the input symbol.  A learned position encoding did not appear to change the model performance either way.

[Tensor2Tensor implementation](https://github.com/tensorflow/tensor2tensor) in TensorFlow.

# Models

Baseline model is $\approx 65$M parameters and has 6 layers, each with 8 self-attention heads using an embedding size of 512.   BLEU scores of 27.3 and 38.1 (EN-DE and EN-FR). Trains 100,000 steps in 12 hours (0.4 s/step) with $\approx 3.3 \times 10^{18}$ FLOPS.

The large model is $\approx 213M$ parameters and has 6 layers, each with 16 self-attention heads using an embedding size of 1024.  BLEU scores of 28.4 and 41.8 (EN-DE and EN-FR). Trains in 300,000 steps in 3.5 days (1 s/step) with $\approx 2.3 \times 10^{19}$ FLOPS.

# Training

Training was done on 8x NVIDIA P100 GPUs.  Baseline model in 12 hours, big model in 3.5 days.  The big model was 4x faster than SOTA at the time.

Model averaging was performed over the last N checkpoints, with checkpoints dropped every 10 minutes.  Baseline model averaged over the 5 checkpoints (7500 steps) and the big model averaged over the last 20 checkpoints (12000 steps).

[[Label Smoothing|Label smoothing]] was used with $\epsilon = 0.1$ to reduce certainty and increase diversity in outputs.  Ultimately this results in improved BLEU scores.

Dropout was used on residual connections with $p = 0.3$ and $p = 0.1$ for the baseline and big models, respectively.

Learning rate schedule has a linear warmup and then a $\frac{1}{\sqrt{step}}$ decay. 

# Ablations and Analysis
The baseline architecture has $N=6$ layers, $d_{model}=512$, and $h = 8$ attention heads, $d_{k} = d_{v} = 64$. 

## Number of Layers
Too few layers hurt the most ($N=2$), though fewer/more layers had minor effects.  This had a larger impact than changing the number of attention heads.

## Number of Attention Heads
Varying $h \in \{1, 4, 16, 32\}$ has less than 1 BLEU point change, with $h = 1$ being the worst. 

## Embedding Sizes
Making embedding sizes larger improved performance.  $d_{model}=4096$ was best for both the baseline and the big model.
