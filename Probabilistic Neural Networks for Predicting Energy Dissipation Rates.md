Tags: #machine-learning #paper-review #fluids #turbulence

# Summary
Pre-print [paper](https://people.umass.edu/debk/Papers/lewin21.pdf) (Lewin, de Bruyn Kops, Portwood, and Caulfield at Cambridge, U Mass, and LLNL) and [code](https://github.com/samlewin/PNN_dissipation).

Simple probabilistic convolutional network learns to compute $\epsilon$ from vertical shear ($S=\frac{\partial u}{\partial z}^2+\frac{\partial v}{\partial z}^2$) and the density gradient ($\frac{\partial \rho}{\partial z}$) which closely matches computed $\epsilon$ from direct numerical simulations (DNS).  This model outperforms the previous model that computed $\epsilon$ from just vertical shear under the assumptions of homogeneous and isotropic turbulence which are incorrect for stratified flows found in the ocean.

Shows that there is information in the density gradient and allows approximation without measuring/computing all 9 partial derivatives needed for directly computing $\epsilon$.

Unclear what the applications of this are since $\epsilon$ isn't directly measured when vertical shear and density gradients are collected.

# Open Questions
1.  What is the target application of this model?  Show that the density gradient is important and the previous model (using only vertical shear) is incorrect for stratified flows?
2. Does this generalize across all turbulence or just specific configurations of Reynolds/Froud/? numbers?
2. How were the training and test data partitioned and sampled?
    - Were the vertical slices in fixed locations (e.g. centered at the turbulence) or random across the column?
    - Why not use all of the temporal snapshots?
    - Were data from a single simulation or multiple?  Which parameters (Re, Fr, ?) were in the datasets?

# Data
Simulation domains are 10m x 10m x 5m (X, Y, Z) with a grid of 4096 x 4096 x 2048.  Turbulence dissipates over 8 buoyance periods (though irregularly sampled at Nt={1, 2, 4, 6, 8}) spanning layered regime (Nt=1) to viscosity dominated, significantly decayed turbulence (Nt=8).

Training data uses 12,000 vertical slices of 500 grid points each (roughly 100 MiB), mapping $S$ to $\epsilon$.  Tested on 500 adjacent vertical slices of 500 grid points.

# Model Architecture
Shallow convolutional network (conv, conv, pool, conv, dense, probabilities, dense) with small filter count (k=32) with roughly 8M parameters.

# Training
Sampled from 5 temporal snapshots (Nt={1, 2, 4, 6, 8}) and trained for 30 epochs in 5 minutes on a Tesla V100.  Adam optimizer with LR=5e-3 using a negative log loss comparing predicted $\epsilon$ against directly computed truth.  

No hyperparameters or architecture search was performed.


# Miscelaneous
$\epsilon$ is the rate at which kinetic energy of turbulence converts to heat by viscous forces at the smallest length scales.
