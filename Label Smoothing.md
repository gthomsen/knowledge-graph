Tags: #machine-learning 

Technique to reduce overfit in a model by making labels less precise.  Can be used to account for label noise so the model doesn't learn the wrong thing.

Hard $0$ and $1$ labels are replaced with $\frac{\epsilon}{k-1}$ and $1 - \epsilon$, where $\epsilon$ is the smoothing parameter and $k$ is the number of classes.  $\epsilon$ can be thought of in terms of the label noise percentage.

