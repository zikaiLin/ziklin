---
editor_options: 
  markdown: 
    wrap: 72
layout: post
title: "Modified Squared Exponential Kernel and Basis Expansion"
author: "Zikai Lin"
classes: wide 
categories:
  - blog
tags:
  - R
  - Plotly
---

## Squared Exponential Kernel

Squared Exponential Kernel, A.K.A, the Radial Basis Function kernel, the
Gaussian kernel. It has the form:
$$
k(x,x') = \sigma^2 \dfrac{\|x-x'\|}{2\rho^2}
$$
It also has only two parameters:

-   The lengthscale, i.e. \(\rho\) controls the smoothness of your kernel.

-   The output variance \(\sigma^2\) determines the 'magnitude' of your
    covariance function. It is like a scale factor.

## Modified Squared Exponential Kernel

We consider modified form of squared-exponential covariance kernel,
defined as:


$$
\kappa(x, x') = \exp\{-a(\|x\| + \|x'\|^2) - b \|x - x'\|^2\},\quad \text{for }a>0, \quad b> 0,
$$




where $$\|\cdot\|$$ is the  $$L_2$$-norm. Notice that $$\kappa(x, x')$$ reduces to standard SE kernel when $$a = 0$$. Here $$a$$ is the decay parameter  controls the decay rate of $$\mathrm{Var}$$

$$\mathrm{Var}\{f_j(\cdot)\}$$ compared to $$\mathrm{Var}\{f_j(0)\}$$. The parameter $b$ is the smoothing parameter of modified SE kernel, smaller value of \(b\) corresponds to a smoother GP $$f_j(\cdot)$$. An important property of modified SE kernel is that it has a closed form eigen decomposition using Hermite polynomials. A $$k$$-th order normalized Hermite polynomials is defined as follow: 


$$
H_k(x) = (2^k k!\sqrt{x})^{1/2}(-1)^k\exp (x^2)\dfrac{d^k}{dx^k}\exp(-x^2),
$$


Mercer's Theorem states that a positive-definite kernel $$k(\mathbf{x},\mathbf{x}')$$ in a finite measure space can be decomposed as 


$$
k(\mathbf{x},\mathbf{x}') = \sum_{i=1}^\infty\lambda_i\phi_{i}(\mathbf{x})\phi_{i}'(\mathbf{x}'),
$$



$$
k(x,x^{'})=\sigma^2\sum^{\infty}_{l=1}\lambda_l\Psi_l(x)\Psi_l(x^{'}) ,
$$


where $$\{\lambda_l\}^{\infty}_{l=1}$$ are eigen values with $$\lambda_l\geq\lambda_{l+1}>0$$ for $$l\geq1$$ and $$\{\phi_l(x)\}^{\infty}_{l=1}$$ are orthonormal eigen functions that satisfy the following properties: $$\int\Psi_l(x)\Psi_l(x^{'})dx=1$$ when $$l=l^{'}$$ and $\int\Psi_l(x)\Psi_l(x^{'})dx=0$ otherwise. The GP $$f_j(\cdot)$$ can then be represented as 


$$
f(x)=\sum^{\infty}_{l=1}\theta_lb_l(x), \quad \theta_l \overset{i.i.d}{\sim} \mathcal{N}(0,\sigma_l^2), \quad \text{for }l = 1,\ldots, \infty
$$


where $$b_l(x)=\sqrt{\lambda_l}\phi_l(x)$$ is the basis function. In practice, we approximate $f_j(\cdot)$ by a truncated eigen-decomposition using $$L$$ basis functions, where $$L$$ is determined by the maximum
polynomial degrees, says $h$, i.e. $$L = \binom{h+d}{d}$$ for $$d$$-dimensional data. 

## Fast Basis Function Expansion based on Eigen Decomposition

In R, there's a nice package called BayesGPfit (Kang) that you can use to do the basis expansion for modified squared-exponential kernel.

Here's an example, consider using basis functions to approximate a modified squared exponential kernel with $$a =0.01$$ and $$b = 1$$:

![pressure-1](/Volumes/easystore/Dropbox (Personal)/GithubPage/ziklin/images/pressure-1.png)

## Reference

Jian Kang (2022). BayesGPfit: Fast Bayesian Gaussian Process Regression Fitting. R package version 1.1.0.
<https://CRAN.R-project.org/package=BayesGPfit>
