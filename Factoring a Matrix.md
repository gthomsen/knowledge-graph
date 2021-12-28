Tags: #linear-algebra #scientific-computing 

# LU Decomposition
For matrices that have no additional structure.  $O(N^3)$ FLOPS to factor $A$ into $L$ and $U$. LAPACK's `getrf()` overwrites $A$ with its factors.

May require an additional pivot array for stability when $A$ is ill-conditioned.

# Cholesky Factorization
For symmetric positive definite matrices. $O(\frac{N^3}{3})$ FLOPS to factor $A$ into $L$ (the other factor isn't required since its the conjugate transpose of $L$).  LAPACK's `potrf()` overwrites $A$ with its factor.

Factorization is stable and doesn't require pivoting.  The entire sequence of computations is deterministic.