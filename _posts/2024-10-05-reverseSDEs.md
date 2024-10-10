---
layout: distill
title: How to Reverse an SDE
description:
tags:
giscus_comments: true
date: 2024-10-07
featured: true

authors:
  - name: Brendan Mallery

bibliography: blog.bib

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
toc:
  - name: Introduction
    # if a section has subsections, you can add them as follows:
    # subsections:
    #   - name: Example Child Subsection 1
    #   - name: Example Child Subsection 2
  - name: Proof of Theorem 2
  - name: Extension to strongly log-concave measures

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
The following derivation is borrowed from <d-cite key="sarkka2019applied"></d-cite>.

Let 
 $$ X_t = b_t(X_t)dt + \sigma_t(X_t)dB_t, \; \; \; \; X_0 \sim \mu_0 $$
 
be a stochastic differential equation, where $b_t \in \mathbb{R}^d$ and $\sigma_t \in \mathbb{R}^{d \times d}$. The Fokker-Planck Equation gives us a way to express the density of $X_t$ as a PDE:
  
**Theorem (Fokker-Planck Equation):** Let $\mu_t = \text{Law}(X_t)$ and $p_t$ be the density of $\mu_t$. Then $p_t$ solves: 
   
$$ \partial \mu_t(x) = - \sum_i \frac{\partial}{\partial x_i} \left( [b_t(x)]_i \mu_t(x) \right) + \frac{1}{2} \sum_{i,j} \frac{\partial^2}{\partial x_i \partial x_j} \left( [\sigma_t(x)\sigma_t^\top(x)]_{ij} \mu_t(x) \right) $$
   
$$ = - \text{div}(b_t(x) \mu_t(x)) + \frac{1}{2} \sum_{i,j} \frac{\partial^2}{\partial x_i \partial x_j} \left( [\sigma_t(x) \sigma_t^\top(x)]_{ij} \mu_t(x) \right) $$
  
  
**Example (Spatially Homogeneous Diffusion):** If $\sigma_t(x)$ is constant as a function of $x$, then this can be written as: 
  
$$ \partial \mu_t(x) = - \text{div}(b_t(x) \mu_t(x)) + \langle \sigma_t \sigma_t^\top, \nabla^2 \mu_t(x) \rangle $$

$$ = - \text{div}(b_t(x)\mu_t(x)) + \sigma_t \sigma_t^\top \nabla \mu_t(x) $$
   
**Example (Langevin Diffusion):** Let $V: \mathbb{R}^d \rightarrow \mathbb{R}$ be continuously differentiable. Then the Fokker-Planck equation is: $$ \partial \mu_t(x) = \text{div}(\nabla V \mu_t) + \frac{1}{2} \Delta \mu_t $$ This has SDE form: $$ X_t = -\nabla V(X_t) dt + dB_t $$ The SDE may be interpreted as a stochastic gradient flow for the function $V$. 
  
*Proof:* Let $\phi \in \mathcal{C}_c^2(\mathbb{R}^d)$. The Ito differential of $\phi(X_t)$ is given by: 
  
$$ d\phi(X_t) = \langle \nabla \phi(X_t), b_t(X_t) \rangle dt + \frac{1}{2} \langle \nabla^2 \phi(X_t), \sigma_t \sigma_t^\top \rangle dt + \langle \sigma_t^\top \nabla \phi(X_t), dB_t \rangle $$
  
Taking expectations and formally dividing both sides by $dt$ gives: 
   
$$ \frac{d E[\phi]}{dt} = \mathbb{E}[\langle \nabla \phi(X_t), b_t(X_t) \rangle] + \frac{1}{2} \mathbb{E}[\langle \nabla^2 \phi(X_t), \sigma_t \sigma_t^\top \rangle] $$
   
The left-hand side can be rewritten as: 
  
$$ \frac{d E[\phi]}{dt} = \frac{d}{dt} \int \phi(x) \mu_t(x) dx = \int \phi(x) \frac{\partial \mu_t(x)}{\partial t} dx $$
  
Recall multidimensional integration by parts: 
   
$$ \int_\Omega \frac{\partial u(x)}{\partial x_i} v(x) dx = \int_{\partial \Omega} u(x) v(x) n_i dS - \int_\Omega u(x) \frac{\partial v(x)}{\partial x_i} dx $$
   
Consider the first term in the equation above, written in coordinate form: 
  
$$ \mathbb{E} \left[ \frac{\partial \phi}{\partial x_i} (X_t) [b_t(X_t)]_i \right] = \int \frac{\partial \phi}{\partial x_i} (x) [b_t(x)]_i \mu_t(x) dx = - \int \phi(x) \frac{\partial}{\partial x_i} \left( [b_t(x)]_i \mu_t(x) \right) dx $$
  
Applying integration by parts, and similarly for the second term: 
   
$$ \mathbb{E} \left[ \langle \nabla^2 \phi(X_t), \sigma_t \sigma_t^\top \rangle \right] = \int \left( \frac{\partial^2 \phi}{\partial x_i \partial x_j} \right) [\sigma_t(x) \sigma_t^\top(x)]_{ij} \mu_t(x) dx $$

$$ = \int \phi(x) \frac{\partial^2}{\partial x_i \partial x_j} \left( [\sigma_t(x) \sigma_t^\top(x)]_{ij} \mu_t(x) \right) dx $$

Substituting these into the earlier equation: 

$$ \int \phi(x) \partial \mu_t(x) dx = - \sum_i \int \phi(x) \frac{\partial}{\partial x_i} \left( [b_t(x)]_i \mu_t(x) \right) dx $$


$$ + \frac{1}{2} \sum_{i,j} \int \phi(x) \frac{\partial^2}{\partial x_i \partial x_j} \left( [\sigma_t(x) \sigma_t^\top(x)]_{ij} \mu_t(x) \right) dx $$

which can be rewritten as: 
$$ \int \phi(x) \left( \frac{\partial \mu_t(x)}{\partial t} + \sum_i \frac{\partial}{\partial x_i} \left( [b_t(x,t)]_i \mu_t(x) \right) - \frac{1}{2} \sum_{i,j} \frac{\partial^2}{\partial x_i \partial x_j} \left( [\sigma_t(x)\sigma_t^\top(x)]_{ij} \mu_t(x) \right) \right) dx = 0 $$

This holds for all $\phi \in \mathcal{C}_c^2(\mathbb{R}^d)$, implying: 

$$ \frac{\partial \mu_t(x)}{\partial t} + \sum_i \frac{\partial}{\partial x_i} \left( [b_t(x,t)]_i \mu_t(x) \right) - \frac{1}{2} \sum_{i,j} \frac{\partial^2}{\partial x_i \partial x_j} \left( [\sigma_t(x)\sigma_t^\top(x)]_{ij} \mu_t(x) \right) = 0 $$

for $\mu_t$ almost every $x$. We will now construct the time reversal of the SDE. Let $X^\leftarrow$ be defined such that $Law(X_t^\leftarrow) = \pi_{T-t}$. For convenience, assume $\sigma_t$ is independent of the spatial variable. The Fokker-Planck equation gives: 

$$ \partial \mu_t^\leftarrow = - \frac{1}{2} \langle \sigma_{T-t} \sigma_{T-t}^\top, \nabla^2 \mu_t^\leftarrow \rangle + \text{div}(\mu_t^\leftarrow b_{T-t}) $$

Observe that: 

$$ \langle \sigma_{T-t} \sigma_{T-t}^\top, \nabla^2 \mu_t^\leftarrow \rangle = \text{div}(\sigma_{T-t} \sigma_{T-t}^\top \nabla \mu_t^\leftarrow) $$

Substituting, the equation becomes: 
$$ \partial \mu_t^\leftarrow = \frac{1}{2} \langle \sigma_{T-t} \sigma_{T-t}^\top, \nabla^2 \mu_t^\leftarrow \rangle + \text{div}(\mu_t^\leftarrow(b_{T-t} - \sigma_{T-t} \sigma_{T-t}^\top \nabla \ln \mu_t^\leftarrow)) $$

The corresponding SDE is: 
$$ dX_t^\leftarrow = \left\{ -b_{T-t}(X_t^\leftarrow) + \sigma_{T-t} \sigma_{T-t}^\top \nabla \ln \mu_t^\leftarrow(X_t^\leftarrow) \right\} dt + \sigma_{T-t} dB_t $$

If initialized at $X_0^\leftarrow \sim \pi_T$, then $X_t^\leftarrow \sim \pi_{T-t}$ for all $t$.