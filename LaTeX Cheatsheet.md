Tags: #cheatsheet 

[Comprehensive list](https://sampig.github.io/tutorial/2019/04/28/learning-latex-mathematical-symbols).

Subset of symbols I use:

| Symbol | Script | Comment |
| --- | --- | --- |
| $\times$ | `\times` | Multiplication "x" |
| $\pm$ | `\pm` | Plus or minus |
| $\circ$ | `\circ` | Degree (**NOTE:** use it as a superscript) |
| $\{$, $\}$ | `\{`, `\}` | Escaped braces |
| $\ne$ | `\ne` |
| $\geq$ | `\geq` | Greater than or equal to |
| $\leq$ | `\leq` | Less than or equal to |
| $\approx$ | `\approx` | Approximately equal to |
| $\lessapprox$ | `\lessapprox` | Approximately less than or equal to |
| $\gtrapprox$ | `\gtrapprox` | Approximately greater than or equal to |
| $\overset{\Delta}{=}$ | `\overset{\Delta}{=}` | Triangle equals |
| $\rightarrow$ | `\rightarrow` | Right arrow |
| $\infty$ | `\infty` | Infinity |
| $\equiv$ | `\equiv` | Equivalence |
| $\hat{X}$ | `\hat{}` | Hat |
| $\nabla$ | `\nabla` | Nabla/del operator |

Forcing the limits of a summation/product/max to be below or above the sigma or pi:

$\sum \limits_{i} A_{i}$ is `\sum \limits_{i} A_{i}`

Writing an underbrace:
$\underbrace{x + \cdots + x}_{n \rm times}$  is `\underbrace{x + \cdots + x}_{n \rm times}`

The size of parentheses, brackets, and braces can be controlled via `\left` + `\right`, `\big`, `\bigg`, and `\Bigg`.

| Expression | Command |
| --- | --- |
| $\left( X + Y \right)$ | `\left( X + Y \right )` |
| $\big( X + Y \big )$ | `\big( X + Y \big )` |
| $\bigg( X + Y \bigg)$ | `\bigg( X + Y \bigg )` |
| $\Bigg( X + Y \Bigg )$ | `\Bigg( X + Y \Bigg )` |

# Formatting

Scripted letters (calligraphic) are done with `\mathcal{...}` like so: $\mathcal{N}$.

Bold letters are done with `\textbf{...}` like so: $\textbf{N}$ vs $N$.

Cursive lower-case $\ell$ is `\ell`.

Recommended ["Short Math Guide for LaTeX"](https://www.math.hkbu.edu.hk/TeX/short-math-guide.pdf) primer.

# Greek Letters
[Wikipedia link](https://en.wikipedia.org/wiki/Greek_alphabet).