---
layout: distill
title: Characterization of KL-divergence Barycenters
description:
tags: ["Information Theory", "Barycenters"]
giscus_comments: true
date: 2025-01-05
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

In this post I'll record a simple but instructive calculation, giving a basic template for characterizing optimizers of functionals on probability space: Let $\Delta^m := \{(\lambda_1, \lambda_2, \dots, \lambda_m) \in \mathbb{R}^m \mid \lambda_j \geq 0, \sum_{j=1}^m \lambda_j = 1\}$ be the $m$-dimensional probability simplex. Let $\mathcal{V} = \{\nu_1, \dots, \nu_m\}$ be a family of probability measures on $\Omega \subseteq \mathbb{R}^d$ such that $\nu_j \propto \exp(-V_j)$ for some nonnegative continuous functions $V_j$. 

For any $\lambda \in \Delta^m$, define $\mathcal{K}_{\lambda, \mathcal{V}}(\mu) := \sum_{j=1}^m \lambda_j\ \mathrm{KL}(\mu \mid \nu_j)$, where $\mathrm{KL}$ denotes the Kullback–Leibler divergence. 

Let $\mu_\lambda := \text{argmin}_{\rho \in \mathcal{P}(\Omega)} \mathcal{K}_{\lambda, \mathcal{V}}(\rho)$. We wish to characterize the set $M := \{\mu_\lambda \mid \lambda \in \Delta^m\}$. 

We will do this using first-order calculus on the space of probability measures.


**Definition 1**  
Let $\mathcal{P}_{\text{abs}}(\Omega) \subseteq \mathcal{P}(\Omega)$ be the set of probability measures which are absolutely continuous with respect to the Lebesgue measure, and let $\mathcal{F} : \mathcal{P}(\Omega) \to \mathbb{R} \cup \{+\infty\}$ be a functional. If $\mathcal{F}(\rho) < \infty$ for all $\rho \in \mathcal{P}_{\text{abs}}(\Omega)$, we say that $\mathcal{F}$ is **regular**.

**Definition 2**  
Let $\mathcal{F}$ be a regular functional, let $\mu \in \mathcal{P}_{\text{abs}}(\Omega)$, and suppose that there exists a continuous function $\frac{\delta \mathcal{F}}{\delta \mu}(\mu): \mathbb{R}^d \to \mathbb{R}$ such that, for all $\rho \in \mathcal{P}_{\text{abs}}(\Omega)$:

$$
\lim_{\epsilon \to 0} \frac{\mathcal{F}(\mu + \epsilon \chi) - \mathcal{F}(\mu)}{\epsilon} = \int \frac{\delta \mathcal{F}}{\delta \mu}(\mu) \, d\chi, \quad \chi := \rho - \mu.
$$

Then we call $\frac{\delta \mathcal{F}}{\delta \mu}(\mu)$ the **first variation** of $\mathcal{F}$ at $\mu$.

The first variation provides a useful necessary condition for optimality:

**Lemma 1**  
Let $\mathcal{F}$ be a regular functional which admits a first variation for all $\mu \in \mathcal{P}_{\text{abs}}(\Omega)$. Suppose that $\mathcal{F}$ admits a minimizer $\mu^\star \in \mathcal{P}_{\text{abs}}(\Omega)$. Then $\frac{\delta \mathcal{F}}{\delta \mu}(\mu^\star)$ is $\mu^\star$-almost everywhere constant.

*Proof:*  
If $\mu^*$ is a minimizer, then for any $\epsilon$ and $\chi := \rho - \mu^*$, we have:

$$
\frac{\mathcal{F}(\mu^* + \epsilon \chi) - \mathcal{F}(\mu^*)}{\epsilon} \geq 0.
$$

Taking the limit as $\epsilon \rightarrow 0$, we get that

$$
\int \frac{\delta \mathcal{F}}{\delta \mu}(\mu^*) \, d\mu^* \leq \int \frac{\delta \mathcal{F}}{\delta \mu}(\mu^*) \, d\rho
$$

for any $\chi$. 

Suppose that $\frac{\delta \mathcal{F}}{\delta \mu}(\mu^\star)$ is not $\mu^\star$-almost everywhere constant. Define $Q := \int \frac{\delta \mathcal{F}}{\delta \mu}(\mu^\star) d\mu^\star$, and let $U := \{x \in \mathbb{R}^d \mid \frac{\delta \mathcal{F}}{\delta \mu}(x) < Q\}$, which is nonempty by assumption. Since $\frac{\delta \mathcal{F}}{\delta \mu}(\mu^\star)$ is continuous, $U$ is measurable. By assumption, $\mu^\star(U) > 0$, and since $\mu^\star$ is absolutely continuous, this implies we may find an absolutely continuous probability measure $\rho$ such that the support of $\rho$ is contained in $U$. Then:


$$
\int \frac{d\mathcal{F}}{d\mu}(\mu^\star) \, d\rho < \int \frac{d\mathcal{F}}{d\mu}(\mu^\star) \, d\mu^\star,
$$

which is a contradiction. Hence $\frac{\delta \mathcal{F}}{\delta \mu}(\mu^\star)$ is $\mu^\star$-almost everywhere constant. $\blacksquare$


We will use the above characterization to describe the set of minimizers of $\mathcal{K}_{\lambda, \mathcal{V}}$. For convenience, let $\Omega$ be compact. We claim that $\mathcal{K}_{\lambda, \mathcal{V}}$ admits a minimizer. This requires an application of Prokhorov's theorem:



**Theorem 1** (Prokhorov's Theorem) Let $(\mathcal{X},d)$ be a complete, compact, separable metric space. Then any sequence of probability measures $\{\mu_n\}_{n=1}^\infty\subseteq \mathcal{P}(\mathcal{X})$ contains a convergent subsequence (in the weak topology).


We remark that the compactness assumption in Theorem 1 can be dropped if the sequence of probability measures is *tight* (in a compact metric space, any $\{\mu_n\}_{n=1}^\infty$ is tight).

**Lemma 2** Let $\Omega\subset \mathbb{R}^d$ be compact, and let $\mathcal{V}=\{\nu_1,..,\nu_m\}\subset \mathcal{P}_{abs}(\Omega)$. Then for any $\lambda\in\Delta^m$, $\mathcal{K}_{\lambda,\mathcal{V}}$ admits an absolutely continuous minimizer.

*Proof:*  
As $KL(-, \nu_j)$ is nonnegative and lower-semicontinuous for all $1 \leq j \leq m$, $\mathcal{K}_{\lambda, \mathcal{V}}$ is as well, and $|\inf_{\rho \in \mathcal{P}(\Omega)} \mathcal{K}_{\lambda, \mathcal{V}}(\rho)| < \infty$. Let $S := \{\mu_n\}_{n=1}^\infty$ be an infimizing sequence for $\mathcal{K}_{\lambda, \mathcal{V}}$. By Theorem 1, $\{\mu_n\}_{n=1}^\infty$ contains a subsequence $\{\mu_n'\}_{n=1}^\infty$, which converges to a limit point $\mu^\star \in \mathcal{P}(\Omega)$. 

As $\mathcal{K}_{\lambda, \mathcal{V}}(\rho) = \infty$ for all $\rho \in \mathcal{P}(\Omega) \setminus \mathcal{P}_{\text{abs}}(\Omega)$, it must be the case that $S \subset \mathcal{P}_{\text{abs}}(\Omega)$. Furthermore, by lower semicontinuity of $\mathcal{K}_{\lambda, \mathcal{V}}$, we have that:

$$
\mathcal{K}_{\lambda, \mathcal{V}}(\mu^\star) \leq \liminf_{n \to \infty} \mathcal{K}_{\lambda, \mathcal{V}}(\mu_n').
$$

This shows that $\mu^\star$ minimizes $\mathcal{K}_{\lambda, \mathcal{V}}$, and furthermore that $\mu^\star \in \mathcal{P}_{\text{abs}}(\Omega)$.

We compute the first variation of

$$
\frac{\delta \mathcal{K}_{\lambda, \mathcal{V}}}{\delta \mu}(\mu) = \sum_{j=1}^m \lambda_j \log\left(\frac{d\mu}{dx}\right) - \sum_{j=1}^m \lambda_j \log\left(\frac{d\nu_j}{dx}\right)
$$

$$
= \log\left(\frac{d\mu}{dx}\right) + \sum_{j=1}^m \lambda_j V_j.
$$

Let $\mu^\star$ minimize $\mathcal{K}_{\lambda, \mathcal{V}}$. Then by Lemma 1, there exists a constant $C$ such that, for (Lebesgue) almost-every $x \in \Omega$:

$$
C = \log\left(\frac{d\mu^\star}{dx}(x)\right) + \sum_{j=1}^m \lambda_j V_j(x)
$$

$$
\Rightarrow \frac{d\mu^\star}{dx}(x) = \exp\left(C - \sum_{j=1}^m \lambda_j V_j(x)\right).
$$

As $\mu^\star$ is a probability measure, its density must integrate to 1, and hence we have (uniquely) identified the constant $C$ as the normalization constant

$$
\ln\left(\int_\Omega \exp\left(-\sum_{j=1}^m \lambda_j V_j(x)\right) dx\right).
$$

We have thus established the theorem:


**Theorem 2** Let $\Omega\subset \mathbb{R}^d$ be compact, and let $\mathcal{V}=\{\nu_1,...,\nu_m\}\subset \mathcal{P}_{abs}(\Omega)$, where for all $1\leq j\leq m$, $\nu_j\propto \exp(-V_j)$ for some continuous and nonnegative $V_j$. Then for any $\lambda\in\Delta^m$:

$$
\texttt{argmin}_{\mu\in \mathcal{P}(\Omega)}\mathcal{K}_{\lambda,\mathcal{V}}(\mu) =\frac{1}{Z_\lambda}\exp\left(-\sum_{j=1}^m\lambda_j V_j\right)
$$

where $Z_\lambda=\int_\Omega \exp(-\sum_{j=1}^m\lambda_j V_j(x))dx$ is a normalization constant.
