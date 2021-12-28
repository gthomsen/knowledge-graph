Tags: #linear-algebra #scientific-computing

Solving $Ax=b$ for $x$ requires at most $N^3$ FLOPS.  Exploiting the structure of $A$ is required for reducing the number of FLOPS required.  See below for common structure and how they're utilized.

If multiple solves with the same $A$ are required then it should be [[Factoring a Matrix|factored]] to dramatically reduce the FLOPS required for each additional $b$.

Derived from:
- [CMU Convex Optimization lecture notes](https://www.stat.cmu.edu/~ryantibs/convexopt-S15/scribes/09-num-lin-alg-scribed.pdf) 
- [Florida State Math 2071 notes](https://people.sc.fsu.edu/~jburkardt/classes/math2071_2020/tridiagonal/tridiagonal.pdf)
# Diagonal
Takes $N$ FLOPS, one for each element-wise division. $x=(b_1/a_1, ..., b_n/a_n)$

# Tridiagonal
Has an $O(9N)$ FLOPS solution that only requires $3N$ entries of $A$ instead of the full $N^2$ matrix.

## Symmetric Positive Definite 
Even more efficient than just a tridiagonal matrix and can be solved in $8N$ FLOPS.

See Golub and van Loan section 4.3.6 for details.

# Triangular
Solved in $N^2$ FLOPS via a forward substitution pass followed by a backward substitution pass (or reversed for using a lower triangular matrix).  

Each pass requires $n$ divisions and $O(\frac{N(N+1)}{2})$ multiplications and additions.

## Cholesky Factor
Solved in $2N^2$ FLOPS. Since $L=L^*$, $y=L^{-1}b$ in $N^2$ FLOPS, and $x=(L^T)^{-1}y$ in $N^2$ FLOPS. 

# Orthogonal
Orthogonality implies $A^{-1}=A^T$ so $x=A^Tb$. So this reduces to a matrix-vector multiplication that is $2n^2$ FLOPS.

# Iterative Solutions
## Non-Symmetric
Use [Generalized Minimum Residual Method](https://en.wikipedia.org/wiki/Generalized_minimal_residual_method) (GMRES).
## Symmetric Positive Definite
Use [Conjugate Gradient](https://en.wikipedia.org/wiki/Conjugate_gradient_method) (CG). Uses less (significantly?) storage than GMRES as well as a 2x faster theoretical convergence rate.
