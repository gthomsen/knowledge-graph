Tags: #compiler-optimizations #performance #scientific-computing 

Strength reduction is the act of replacing expensive operations with equivalent but less expensive operations.  Requires constant loop invariants and that the induction variables must change by known amounts.

Examples include:
- Replacing a looped multiplication with additions
- Replacing a looped exponentiation with multiplications
- Replacing multiplications or divisions with equivalent bit shifts

Strength reductions may not produce identical results as the original code due to rounding.

Original code:
```c
c = 7;
for( i = 0; i < N; i++ )
{
    y[i] = c * i;
}
```

With strength reductions the above can be transformed to:
```c
c = 7;
k = 0;
for( i = 0; i < N; i++ )
{
    y[i]  = k;
    k    += c;
}
```

Derived from [Wikipedia](https://en.wikipedia.org/wiki/Strength_reduction).