---
layout: distill
title: Kernel Ridge Regression
description: asdfasdf
tags: ["Convex Optimization","Dictionary Learning","Regularization"]
giscus_comments: true
date: 2024-11-24
featured: false

authors:
  - name: Brendan Mallery

bibliography: blog.bib

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
#toc:
#  - name: Convexity
#  - name: Ricci Curvature
#  - name: Convexity Meets Curvature


# Below is an example of injecting additional post-specific styles.
# If you use this post as a template, delete this _styles block.
_styles: >
  .fake-img {
    background: #bbb;
    border: 1px solid rgba(0, 0, 0, 0.1);
    box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
    margin-bottom: 12px;
  }
  .fake-img p {
    font-family: monospace;
    color: white;
    text-align: left;
    margin: 12px 0;
    text-align: center;
    font-size: 16px;
  }
---

## Constructing Reproducing Kernel Hilbert Spaces

**Definition 1** Let $\mathcal{X}$ be a metric space. A positive semidefinite kernel is a symmetric function $\mathcal{K}:\mathcal{X}\times \mathcal{X}\rightarrow \mathbb{R}$ such that for all $\{x_i\}_{i=1}^n\subset \mathcal{X}$, the matrix $K_{ij}:=\mathcal{K}(x_i,x_j)$ is PSD.


**Example 1**
Let $\mathcal{X}=\mathbb{R}^d$, $\mathcal{K}(x,x')=\langle x,x'\rangle$. Let $\{x_i\}_{i=1}^n$ be an arbitrary set of points. Then for any vector $\alpha\in \mathbb{R}^d$, we have:
\begin{equation*}
\alpha^\top K \alpha=\sum_{i,j=1}^n\alpha_i\alpha_j\langle x_i,x_j\rangle=\|\sum_{i=1}^n \alpha_i x_i\|^2\geq 0
\end{equation*}


**Example 2** Let $\mathcal{X}=\mathcal{P}_2(\mathbb{R}^d)$. For any $\rho\in \mathcal{P}_2(\mathbb{R}^d)$, define the function $\mathcal{K}_\rho(\mu,\nu)=\langle Id-T_{\rho\rightarrow \mu}, Id-T_{\rho\rightarrow \nu}\rangle _{L^2(\rho)}$. Then for any $\mathcal{V}:=\{\nu_1,...,\nu_m\}$, $K_\mathcal{V}$ is PSD.  

## Function Interpolation

We want to solve the following problem: 


**Problem 1** (Minimal Norm Interpolation) Let $\mathcal{D}:=\{(x_i,y_i)\}_{i=1}^n$ be data-response pairs, where $x_i\in \mathcal{X}$ and $y_i\in \mathbb{R}$. Let $\mathcal{A}_\mathcal{D}\subset \mathcal{H}_\mathcal{K}$ be the set of functions such that $f(x_i)=y_i$ for all $1\leq i\leq n.$ Choose $\bar{f}\in \texttt{argmin}_{f\in \mathcal{A}_\mathcal{D}}\|f\|_{\mathcal{H}_\mathcal{K}}$. 


In the RKHS case, this problem is greatly simplified.



**Proposition 1** 
Let $\mathcal{K}$ be a kernel on $\mathcal{X}$, let $K\in \mathbb{R}^{n\times n}$ be the matrix defined
\begin{equation*}
K_{ij}=\frac{1}{n}\mathcal{K}(x_i,x_j).
\end{equation*}
Then Problem 1 is feasible iff $y=(y_1,...,y_n)\in \text{range}(K)$. If this holds, then the optimal solution can be written:
\begin{equation*}
\hat{f}(-)=\frac{1}{\sqrt{n}}\sum_{i=1}^n \hat{\alpha}_i \mathcal{K}(-,x_i), \; \; \; \; K\hat{\alpha}=\frac{y}{\sqrt{n}}
\end{equation*}
where $\hat{\alpha}\in \mathbb{R}^n.$

*Proof:*

For any vector $ \alpha \in \mathbb{R}^n $, define

$$
\mathcal{F} := \left\{ f_\alpha(-) := \frac{1}{\sqrt{n}} \sum_{i=1}^n \alpha_i \mathcal{K}(-, x_i) \right\}.
$$

For any $ f_\alpha \in \mathcal{F} $, we have:

$$
f_\alpha(x_j) = \frac{1}{\sqrt{n}} \sum_{i=1}^n \alpha_i \mathcal{K}(x_j, x_i) = \sqrt{n} [K\alpha]_j,
$$

i.e., $ \sqrt{n} $ times the $ j $-th entry of $ K\alpha $. Hence, $ f_\alpha \in \mathcal{F} $ solves Problem 1 if and only if

$$
K\alpha = \frac{y}{\sqrt{n}}.
$$

We conclude by showing that the solution must be in $ \mathcal{F} $: Given any $ f \in \mathcal{H}_\mathcal{K} $, we can decompose

$$
f = f_\alpha + f_\perp,
$$

where $ f_\alpha \in \mathcal{F} $ and $ f_\perp \in \mathcal{F}^\perp $ (since $ \mathcal{F} $ is finite-dimensional and hence closed, this decomposition is always possible). By the reproducing property, we have:


$$
f(x_j) = \langle f, \mathcal{K}(-, x_j) \rangle_{\mathcal{H}_\mathcal{K}} = \langle f_\alpha + f_\perp, \mathcal{K}(-, x_j) \rangle_{\mathcal{H}_\mathcal{K}} = f_\alpha(x_j),
$$

since \( \mathcal{K}(-, x_j) \in \mathcal{F} \) and is hence orthogonal to \( f_\perp \). This, along with the fact that

$$
\|f_\alpha + f_\perp\|^2_{\mathcal{H}_\mathcal{K}} = \|f_\alpha\|^2_{\mathcal{H}_\mathcal{K}} + \|f_\perp\|^2_{\mathcal{H}_\mathcal{K}},
$$

implies that the solution must lie in \( \mathcal{F} \), if it exists. \blacksquare


We now consider a harder problem: Suppose we observe $n$-i.i.d. data points $y_i=f^*(x_i)+w_i$ where $f$ is some function of data $x_i$ and $w=(w_1,...,w_n)$ is a noise vector. We will solve this via a relaxation of the previous method:


**Problem 2**
(Kernel ridge regression) For some $\lambda_n>0$, define, find: 

\begin{equation*} \hat{f}=\texttt{argmin}_{f\in \mathcal{H}_\mathcal{K}}\left\{\frac{1}{2n}\sum_{i=1}^n(y_i-f(x_i))^2+\lambda_n \|f\|^2_{\mathcal{H}_\mathcal{K}}\right\}\end{equation*}

**Proposition 2**
For all $\lambda_n>0$, Problem 2 can be written as:
\begin{equation}\label{eqn:krr solution}
\hat{f}(-)=\frac{1}{\sqrt{n}}\sum_{i=1}^n\hat{\alpha}_i\mathcal{K}(-,x_i),
\end{equation}
where the optimal weight vector $\hat{\alpha}\in \mathbb{R}^n$ is given by:
\begin{equation*}
\hat{\alpha}=(K+\lambda_n I_n)^{-1}\frac{y}{\sqrt{n}}.
\end{equation*}

*Proof:*
The formula for the optimal $\hat{f}$ follows the same reasoning as in the previous proof. To compute the optimal weight vector, first notice that for any function $f$ of the above form, for each $j = 1, 2, ..., n$ we have:

$$
f(x_j) = \frac{1}{\sqrt{n}} \sum_{i=1}^n \alpha_i \mathcal{K}(x_j, x_i) = \sqrt{n} \, e_j^\top K \alpha,
$$

where $e_j$ is a basis vector and $K_{ij} = \mathcal{K}(x_i, x_j)/n$. Similarly, we have:

$$
\|f\|^2_{\mathcal{H}_\mathcal{K}} = \frac{1}{n} \left\langle \sum_{i=1}^n \alpha_i \mathcal{K}(-, x_i), \sum_{j=1}^n \alpha_j \mathcal{K}(-, x_j) \right\rangle_{\mathcal{H}_\mathcal{K}} = \alpha^\top K \alpha.
$$

Plugging these into the cost function we get:

$$
\frac{1}{2n} \sum_{i=1}^n \left( y_i - \sqrt{n} [K \alpha]_i \right)^2 + \lambda_n \|f\|^2_{\mathcal{H}_\mathcal{K}} = \frac{1}{n} \|y - \sqrt{n} K \alpha\|^2_2 + \lambda \alpha^\top K \alpha,
$$

which expands to:

$$
\frac{1}{n} \|y\|^2_2 + \alpha^\top (K^2 + \lambda K) \alpha - \frac{2}{\sqrt{n}} y^\top K \alpha.
$$

Taking the gradient with respect to $\alpha$ and setting it equal to zero, we get:

$$
K(K + \lambda I_n)\alpha - \frac{1}{\sqrt{n}} K y = 0,
$$

which implies:

$$
K(K + \lambda I_n)\alpha = \frac{1}{\sqrt{n}} K y.
$$

Solving for $\alpha$ gives us our solution.

\blacksquare