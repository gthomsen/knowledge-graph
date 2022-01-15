Optimal transport is an assignment problem with applications like:
- Mapping deserts to people with preferences
- Mapping raw materials to production facilities
- [[An Image is Worth 16x16 Words - Transformers for Image Recognition at Scale|Assigning N-dimensional vectors to K-many clusters]]

Michiel Stock has a [great explanation by example](https://michielstock.github.io/posts/2017/2017-11-5-OptimalTransport) on how optimal transport works.  His diagram on how the cost matrix, $M$, relates to the set of all feasible distributions, $U(\textbf{r}, \textbf{c})$, and how $\lambda$ relaxes the constraints, the black polygon relaxes to the red oval, to make finding an optimum easier, $P_{\lambda}^{*}$ instead of $P^{*}$.  Under $M$, $P^{*}$ is the optimum, while $\textbf{rc}^T$ is homogeneous distribution (equal assignment ignoring the costs).  As $\lambda \rightarrow \infty$, $P_{\lambda}^{*} \rightarrow P^{*}$.  As $\lambda \rightarrow 0$, $P_{\lambda}^{*} \rightarrow \textbf{rc}^T$.

![BLAH](https://michielstock.github.io/images/2017_optimal_transport/geometry.png)

The paper "[[Sinkhorn Distances - Lightspeed Computation of Optimal Transport Distances|Sinkhorn Distances: Lightspeed Computation of Optimal Transport Distances]]" by Cuturi (2013) gives an efficient implementation.