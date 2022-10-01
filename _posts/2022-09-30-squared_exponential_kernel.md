## Squared Exponential Kernel

Squared Exponential Kernel, A.K.A, the Radial Basis Function kernel, the
Gaussian kernel. It has the form:

$$k(x,x') = \sigma^2 \dfrac{\\|x-x'\\|}{2\rho^2}$$

It also has only two parameters:

-   The lengthscale, i.e. *ρ* controls the smoothness of your kernel.

-   The output variance *σ*<sup>2</sup> determines the ‘magnitude’ of
    your covariance function. It is like a scale factor.

## Modified Squared Exponential Kernel

For all numerical experiments conducted in our analysis, we consider
modified form of squared-exponential covariance kernel, defined as:

*κ*(*x*,*x*′) = exp { − *a*(∥*x*∥+∥*x*′∥<sup>2</sup>) − *b*∥*x* − *x*′∥<sup>2</sup>},  for *a* &gt; 0,  *b* &gt; 0,

where ∥ ⋅ ∥ is the *L*<sub>2</sub>-norm. Notice that *κ*(*x*,*x*′)
reduces to standard SE kernel when *a* = 0. Here *a* is the decay
parameter controls the decay rate of Var{*f*<sub>*j*</sub>(⋅)} compared
to Var{*f*<sub>*j*</sub>(0)}. The parameter *b* is the smoothing
parameter of modified SE kernel, smaller value of *b* corresponds to a
smoother GP *f*<sub>*j*</sub>(⋅). An important property of modified SE
kernel is that it has a closed form eigen decomposition using Hermite
polynomials. A *k*-th order normalized Hermite polynomials is defined as
follow:
$$H\_k(x) = (2^k k!\sqrt{x})^{1/2}(-1)^k\exp (x^2)\dfrac{d^k}{dx^k}\exp(-x^2),$$
Mercer’s Theorem states that a positive-definite kernel
*k*(**x**,**x**′) in a finite measure space can be decomposed as %
$$k(\mathbf{x},\mathbf{x}') = \sum\_{i=1}^\infty\lambda\_i\phi\_{i}(\mathbf{x})\phi\_{i}'(\mathbf{x}'),$$
$$k(x,x^{'})=\sigma^2\sum^{\infty}\_{l=1}\lambda\_l\Psi\_l(x)\Psi\_l(x^{'}) ,$$
where {*λ*<sub>*l*</sub>}<sub>*l* = 1</sub><sup>∞</sup>are eigen values
with *λ*<sub>*l*</sub> ≥ *λ*<sub>*l* + 1</sub> &gt; 0 for *l* ≥ 1 and
{*ϕ*<sub>*l*</sub>(*x*)}<sub>*l* = 1</sub><sup>∞</sup> are orthonormal
eigen functions that satisfy the following properties:
∫*Ψ*<sub>*l*</sub>(*x*)*Ψ*<sub>*l*</sub>(*x*<sup>′</sup>)*d**x* = 1 when
*l* = *l*<sup>′</sup> and
∫*Ψ*<sub>*l*</sub>(*x*)*Ψ*<sub>*l*</sub>(*x*<sup>′</sup>)*d**x* = 0
otherwise. The GP *f*<sub>*j*</sub>(⋅) can then be represented as
$$f(x)=\sum^{\infty}\_{l=1}\theta\_lb\_l(x), \quad \theta\_l \overset{i.i.d}{\sim} \mathcal{N}(0,\sigma\_l^2), \quad \text{for }l = 1,\ldots, \infty$$
where $b\_l(x)=\sqrt{\lambda\_l}\phi\_l(x)$ is the basis function. In
practice, we approximate *f*<sub>*j*</sub>(⋅) by a truncated
eigen-decomposition using *L* basis functions, where *L* is determined
by the maximum polynomial degrees, says *h*, i.e. $L = \binom{h+d}{d}$
for *d*-dimensional data.

## Fast Basis Function Expansion based on Eigen Decomposition

In R, there’s a nice package called BayesGPfit (Kang) that you can use
to do the basis expansion for modified squared-exponential kernel.

Here’s an example, consider using basis functions to approximate a
modified squared exponential kernel with *a* = 0.01 and *b* = 1:
![](2022-09-30-squared_exponential_kernel_files/figure-markdown_strict/pressure-1.png)

## Reference

Jian Kang (2022). BayesGPfit: Fast Bayesian Gaussian Process Regression
Fitting. R package version 1.1.0.
<https://CRAN.R-project.org/package=BayesGPfit>
