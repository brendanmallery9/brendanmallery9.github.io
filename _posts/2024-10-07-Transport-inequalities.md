---
layout: distill
title: Notes on Transportation Inequalities
description: 
tags: ["Optimal Transport", "Concentration of Measure", "Transportation Inequalities"]
giscus_comments: true
date: 2024-10-07
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

Here are some notes from back when I was trying to really learn about transport inequalities for the first time. Most of the following is distilled from <d-cite key="gozlan2010transport"></d-cite> and <d-cite key="gozlan2015transport"></d-cite>. Before going ahead, I'll say that since then there have been a number of times where I was working hard on something, only to realize that what I ``really doing'' the whole time was establishing a transport inequality. I mention this because (in my opinion), transport inequalities seem opaque and technical when you first come across them, made all the more mysterious by the fact that a lot of the most [celebrated results](https://cedricvillani.org/sites/dev/files/old_images//2012/08/014.OV-Talagrand.pdf) in the field are about establishing them. 

So if you are like me and are not particularly motivated by a bunch of statements like "LSI==> T2 ==> T1", rest assured that these things become unexpectedly handy, unexpectedly often.

## Introduction

**Definition 1:** (Transport Inequality) Let $\mathcal{X}$ be a Polish space equipped with a cost function $c:\mathcal{X}^2\rightarrow \mathbb{R}$ with $c(x,x)=0$ for all $x\in \mathcal{X}$. Consider a function $J(-\mid-):\mathcal{P}(\mathcal{X})^2\rightarrow [0,\infty]$ and $\alpha:[0,\infty)\rightarrow [0,\infty)$ an increasing function so that $\alpha(0)=0.$ Then $\mu\in \mathcal{P}(\mathcal{X})$ satisfies the transport inequality $\alpha(\mathcal{T}_c)\leq J$ if:

$$
\alpha(\mathcal{T}_c(\nu,\mu))\leq J(\nu\mid\mu), \forall \nu\in\mathcal{P}(\mathcal{X})
$$


We will primarily concerned with the following family of examples:

  

**Definition 2:** (Transport-Entropy Inequality) Let $(\mathcal{X},d)$ be a metric space and let $C>0$. We say that $\mu$ satisfies the inequality $T_p(C)$ if:

$$
W^2_p(\mu,\nu)\leq CH(\nu\mid\mu)
$$

where $W_p$ is the $p$-Wasserstein distance and $H$ is the relative entropy.

  

We will typically take $p=1,2$. When $p=1$, this is Definition 1 with $\alpha(x)=\frac{1}{C}x^2$. When $p=2$, this is Definition 1 with $\alpha(x)=\frac{1}{C}x$. Observe by Jensen's inequality, $T_1(C)$ is always weaker than $T_2(C).$ A basic example is the following:


**Theorem 1:** (Pinsker's Inequality ) Let $\mu,\nu \in \mathcal{P}(\mathcal{X})$, and let $d_H$ denote the Hamming distance. Then:

$$
\mathcal{T}^2_{d_H}(\mu,\nu)=\|\mu-\nu\|^2_{TV}\leq \frac{1}{2}H(\nu\mid\mu)
$$

where $\|.\|_{TV}$ denotes the total-variation distance.

A particularly famous one was proven by Talagrand:

**Theorem 2:** ($T_2$ for the Standard Gaussian) The standard Gaussian measure $\gamma$ on $\mathbb{R}^d$ satisfies $T_2(2)$, and this constant is sharp.
\end{mytheo}

Before proving Theorem 2, we mention some applications:

*Applications of transportation inequalities:*
1. If $\mu$ satisfies a transportation inequality, it is concentrated w.r.t. that cost function. $T_2$ is particularly useful in that it ''tensorizes'', allowing one to establish \textit{dimension independent} concentration for $\mu^{\otimes n}$.
2. Transportation inequalities can allow one to prove other functional inequalities of interest.
3. Connections to positive curvature lower bounds

We will see an example of $T_2$ implying tensorization later. First, we will elaborate on the connection to concentration, via a proof attributed to [Katalin Marton](https://en.wikipedia.org/wiki/Katalin_Marton):

**Theorem 3** (Marton's argument) Let $\alpha: \mathbb{R}^+\rightarrow \mathbb{R}^+$ be bijective, and suppose that $\mu\in \mathcal{P}(\mathcal{X})$ satisfies $\alpha(\mathcal{T}_{d^p})\leq H$ for $p\geq 1$. Then for all measurable $A\subset \mathcal{X}$ with $\mu(A)\geq \frac{1}{2}$, the following concentration inequality holds:

$$
\mu(\{x\in \mathcal{X}\mid d(x,A)\leq r\}) \geq 1-e^{-\alpha(r-r_0)},
$$

for all $r>r_0:=\alpha^{-1}(\log(2))$. Equivalently, for all $1$-Lipschitz $f$, the following holds:

$$
\mu(\{f>m_f+r+r_0\})\leq e^{-\alpha(r)},\;\;\;\;\;\;r\geq 0
$$

where $m_f$ is the median of $f$. 

*Proof:* Take $A\subset \mathcal{X}$ with $\mu(A)\geq \frac{1}{2}$, and let $B=\mathcal{X}\setminus A^r$. Consider $d\mu_A(x):=\frac{1}{\mu(A)}1_A(x) d\mu(x)$ and $d\mu_B=1_B(x)d\mu(x)$. Any coupling between $\mu_A$ and $\mu_B$ has cost lower bounded by $r$, by definition. Via the triangle inequality we have :

$$
\begin{align*}
r & \leq \mathcal{T}_{d^p}(\mu_A,\mu_B) \\& \leq \mathcal{T}_{d^p}(\mu_A,\mu)+\mathcal{T}_{d^p}(\mu_B,\mu) \\ & \leq \alpha^{-1}(H(\mu_A\mid\mu)) +\alpha^{-1}(H(\mu_B\mid\mu)).
\end{align*}
$$

We compute:

$$ 
\begin{align*}
H(\mu_A\mid\mu) & = \int \log (\frac{d\mu_A}{d\mu})d\mu_A \\ & = \frac{1}{\mu(A)}\int_A \log(\frac{1}{\mu(A)})d\mu \\& = -\log (\mu(A)) \\&  \leq \log 2
\end{align*} 
$$

and 
$$ 
\begin{align*}
H(\mu_B\mid\mu) & = \frac{1}{\mu(B)}\int_B \log(\frac{1}{\mu(B)})d\mu \\ & = -\log(1-\mu(A^r))
\end{align*} 
$$

Applying $\alpha$ and exponentiating both sides, we obtain:

$$
\begin{equation*}
\mu(A^r)\geq 1- e^{-\alpha(r-r_0)}
\end{equation*} 
$$
for all $r\geq r_0$.

Hence we see $T_p\rightarrow$ subgaussian concentration for any $p$. Observe that from the above, __there is no apparent difference between $T_2$ and $T_1$, as both imply subgaussian concentration.__

## Proof of Theorem 2

In this section we give a proof of Theorem 2. The strategy will be to prove the result in 1-D then to use \textit{tensorization} properties of $T_2$.

**Lemma 1:** Let $V: \mathbb{R}\rightarrow \mathbb{R}_{\geq 0}$, and let $\mu\in \mathcal{P}_2(\mathbb{R})$ be defined by $d\mu(x)=e^{-V(x)}dx$. Then: 

$$
H(\nu\mid\mu)\geq \int V(T_{\mu\rightarrow \nu}(x))-V(x)-V'(x)[T_{\mu\rightarrow \nu}(x)-x] d\mu(x)
$$

where $T_{\mu\rightarrow \nu}$ is the optimal transport map from $\mu$ to $\nu$. 

*Proof:* By Brenier's theorem, $T_{\mu\rightarrow \nu}$ is a monotone map. Assume that $f$ is absolutely continuous and hence we have $\nu=f\mu$. We may write 

$$
\nu((-\infty,T_{\mu\rightarrow \nu}(x)])=\mu((-\infty,x])
$$

for all $x\in \mathbb{R}$. By definition of pushforwards, this means:
$$
\int_{-\infty}^{T_{\mu\rightarrow \nu}(x)} f(z)e^{-V(z)} dz=\int_{-\infty}^x e^{-V(z)}dz.
$$

Differentiating, we have:
$$ 
f(T_{\mu\rightarrow \nu}(x))e^{-V(T_{\mu\rightarrow \nu}(x))}T'_{\mu\rightarrow \nu}(x)=e^{-V(x)}.
$$

Taking logarithms, we get:
$$
\log f(T_{\mu\rightarrow \nu}(x))+\log T'_{\mu\rightarrow \nu}(x) -V(T_{\mu\rightarrow \nu}(x))=-V(x).
$$

Integrating both sides w.r.t. $\mu$, we get:
$$
\begin{align*}
\int \log f d\nu & =  \int (V(T_{\mu\rightarrow \nu}(x))-V(x) - \log T'_{\mu\rightarrow \nu}(x))e^{-V(x)}dx 
\end{align*}
$$

By integration by parts, we have: $\int (T_{\mu\rightarrow \nu}(x)-x)V'(x) e^{-V(x)}dx=\int (T'_{\mu\rightarrow \nu}(x)-1)e^{-V(x)}dx.$ Adding and subtracting this to the above equation we get:

$$
\begin{align*}
\int \log f d\nu & = \int (V(T_{\mu\rightarrow \nu}(x))-V(x)-V'(x)[T_{\mu\rightarrow \nu}(x)-x])d\mu(x) +\int T'_{\mu\rightarrow \nu}(x)-1 -\log T'_{\mu\rightarrow \nu}(x) d\mu(x) \\ & \geq \int V(T_{\mu\rightarrow \nu}(x))-V(x)-V'(x)[T_{\mu\rightarrow \nu}(x)-x]d\mu
\end{align*}
$$

since $b-1-\log b\geq 0$ for all $b>0$. The left hand side is $H(\nu\mid\mu)$ and we are done. 

**Corollary 1:** ($T_1$ for the standard 1D Gaussian) Let $\gamma$ be the standard 1-D Gaussian. Then $\gamma$ satisfies $T_2(2)$:

$$
H(\nu\mid\mu)\geq \frac{1}{2} W_2^2(\nu,\gamma)
$$

*Proof:* Applying Lemma 1 with $V(x)=x^2/2+\log(2\pi)/2$ we get:
$$
H(\nu\mid\gamma)\geq \int \frac{(T_{\gamma\rightarrow \nu}(x)-x)^2}{2} d\gamma(x) = \frac{W_2^2(\nu,\gamma)}{2}.
$$

We remark that the general case may be proven by generalizing the above argument. Instead, we proceed by establishing the tensorization property for transport inequalities. First we define infimum convolution:

**Definition:** Let $\alpha_1,\alpha_2 : [0,\infty)\rightarrow [0,\infty)$. Then the infimum convolution of $\alpha_1,\alpha_2$ is defined:
$$
\alpha_1 \square \alpha_2(t)=\inf \{\alpha_1(t_1)+\alpha_2(t_2):t_1+t_2=t\}.
$$

**Remark:**
- Infimal-convolution is integral convolution in the min-plus algebra
- Infimum-convolution preserves convexity. 
- If $\alpha_1,\alpha_2$ are increasing then $\alpha_1\square \alpha_2$ is as well.
- The proximal operator $\text{prox}^\mu_f(x)=\inf_w f(x)+\frac{1}{2\mu}\|x-w\|^2$ is an example of an infimal-convolution.
- Note we may write Kantorovich duality as:
$$
W_p(\mu,\nu)^p=\displaystyle\sup_{f \in C_b(\mathcal{\mathbb{R}^d})} \int f\square \|.\|^p d\nu - \int f d\mu.
$$

- **Important:** For convex, increasing $\alpha$, we have: $\alpha^{\square n}(t)=n \alpha (t/n)$ for all $t\geq 0$. (Proof: Set $n=2$ and take a derivative, then generalize.)

**Theorem 4:** Suppose $\mu$ verifies $T_1(C)$ on $(\mathcal{X},d)$. Then $\mu^{\otimes n}$ verifies the inequality $T_1(nC)$ on $\mathcal{X}^n$ equipped with $d_1^n(x,y):=\sum_{i=1}^n d(x_i,y_i)$. Consequently, for all $1$-Lipschitz functions $f$:

$$
n \alpha\left(\frac{\mathcal{T}_{c^{\oplus n}} (\nu,\mu^{\otimes n})}{n}\right) \leq H(\nu\mid\mu^{\otimes n}),
$$

for all $\nu\in \mathcal{P}(\mathcal{X}^n)$, where $c^{\oplus n}(x,y)=\sum_{i=1}^n c(x_i,y_i)$.

*Proof:* We will prove this for $n=2$, and the result extends to arbitrary $n$ by induction: Let $\nu\in \mathcal{P}(\mathcal{X}\times \mathcal{X})$. Then we may define the conditional expectation w.r.t. the first coordinate as follows:
$$
d\nu(x_1,x_2)=d\nu_1(x_1)d\nu_2^{x_1}(x_2).
$$

With this notation established, we establish some useful facts:
$$
\begin{equation}\mathcal{T}_{c_1\otimes c_2}(\nu,\mu_1\otimes \mu_2)\leq \mathcal{T}_{c_1}(\nu_1,\mu_1)+\int \mathcal{T}_{c_2}(\nu_2^{x_1},\mu_2)d\nu_1(x_1),\label{eqn:transport_tensor}
\end{equation}
$$

$$
\begin{equation}H(\nu\mid\mu_1\otimes \mu_2)=H(\nu_1\mid\mu_1)+\int H(\nu_2^{x_1}\mid\mu_2)d\nu_1(x_1)\label{eqn:entropy_tensor}
\end{equation}
$$

(\ref{eqn:transport_tensor}) is established via the coupling that transports ''optimally on slices'' of $\nu$ and $\mu_1\otimes \mu_2$. (\ref{eqn:entropy_tensor}) is a famous property known as the disintegration of entropy. We compute:

$$
\begin{align*}
\alpha_1\square \alpha_2 (\mathcal{T}_{c_1\oplus c_2}(\nu,\mu_1\otimes\mu_2) &\leq \alpha_1\square \alpha_2\left(\mathcal{T}_{c_1}(\nu_1,\mu_1)+\int \mathcal{T}_{c_2}(\nu_2^{x_1},\mu_2)d\nu_1(x_1)\right)\\ &\leq \alpha_1(\mathcal{T}_{c_1}(\nu_1,\mu_1))+\alpha_2\left(\int \mathcal{T}_{c_2}(\nu_2^{x_1},\mu_2)d\nu_1(x_1)\right) \\ & \leq \alpha_1(\mathcal{T}_{c_1}(\nu_1,\mu_1))+\int \alpha_2(\mathcal{T}_{c_2}(\nu_2^{x_1},\mu_2))d\nu_1(x_1)\\& \leq H(\nu_1\mid\mu_1)+\int H(\nu_2^{x_1}\mid\mu_2)d\nu_1(x_1) \\& = H(\nu\mid\mu_1\otimes \mu_2)
\end{align*}
$$

where we used the fact that $\alpha_1\square \alpha_2$ is increasing, the definition of infimal-convolution and Jensen's inequality, along with (\ref{eqn:transport_tensor}) and (\ref{eqn:entropy_tensor}).

Let's specialize this to our typical cost functions:

**Corollary 2:** (Tensorization of $T_1$) Suppose $\mu$ verifies $T_1(C)$ on $(\mathcal{X},d)$. Then $\mu^{\otimes n}$ verifies the inequality $T_1(nC)$ on $\mathcal{X}^n$ equipped with $d_1^n(x,y):=\sum_{i=1}^n d(x_i,y_i)$. Consequently, for all $1$-Lipschitz functions $f$:

$$
\begin{equation*}
\mu^{\otimes n}(f>m_f+r+r_0)\leq e^{-\frac{r^2}{nC}}
\end{equation*}
$$

for $r\geq r_0=\sqrt{n C\log(2)}$.

*Proof:* $T_1(C)$ means:

$$
W_1^2(\nu,\mu)=\mathcal{T}^2_d(\nu,\mu)\leq CH(\nu\mid\mu),
$$

and hence $\frac{1}{n}\mathcal{T}^2_{d_1^n}(\nu,\mu)\leq CH(\nu\mid\mu)$ (recall that $\alpha(x)=\frac{1}{C}x^2$ in this case). Apply Theorem 4 and Theorem 3 to conclude concentration.


**Corollary 3:** (Tensorization of $T_2$) Suppose $\mu$ verifies $T_2(C)$ on $(\mathcal{X},d)$. Then $\mu^{\otimes n}$ verifies the inequality $T_2(C)$ on $\mathcal{X}^n$ equipped with $d_2^n(x,y)=\sqrt{\sum_{i=1}^n d^2(x_i,y_i)}$. Consequently, for all $1$-Lipschitz functions $f$:

$$
\begin{equation*}
\mu^{\otimes n}(f>m_f+r+r_0)\leq e^{-\frac{r^2}{C}}
\end{equation*}
$$

for $r\geq r_0=\sqrt{2\log 2}$.

*Proof:* $T_2(C)$ means:

$$
W_2^2(\nu,\mu)=\mathcal{T}_{d_2^1}(\nu,\mu)\leq CH(\nu\mid\mu).
$$

 In this case, $\alpha=\frac{1}{C}$, so Theorem 4 yields: 

$$
\mathcal{T}_{\sum_{i=1}^n d^2}(\nu,\mu^{\otimes n})\leq CH(\nu\mid\mu^{\otimes n}).
$$

Observe that:

$$
\mathcal{T}_{\sum_{i=1}^n d^2}=\mathcal{T}_{(d_2^n)^2}(\nu,\mu^{\otimes n})
$$

and hence this is $T_2(C)$ with this metric.  


Hence we see that $T_2$ is much stronger than $T_1$, since it tensorizes to give dimension free concentration. Combining Corollary 3 and Corollary 1, we obtain Theorem 2.


### Extension to strongly log-concave measures

Suppose $\mu\in \mathcal{P}(\mathcal{X})$ satisfies $\mu(f>m_f+r+r_0)\leq \ell(r)$ for some $r_0$ and decreasing function $\ell(r)$, for all 1-Lipschitz functions $f$ (i.e. $\mu$ has concentration profile $\ell$). Suppose further that $\nu\in \mathcal{P}(\mathcal{X})$ and that there exists a $1$-Lipschitz transport map $T_{\mu\rightarrow \nu}$ pushing $\mu$ onto $\nu$. Then it is clear that $\nu( f > m_f +r +r_0)\leq \ell(r)$ as well. To see this, observe that for any measurable $A\subset \mathcal{X}$ with $\mu(A)\geq \frac{1}{2}$ we have $\nu(T_{\mu\rightarrow \nu}(A))\geq \frac{1}{2}$ by definition of a transport map, and furthermore that:

$$
\begin{align*}
1-\ell(r)& \leq \mu(A^r) \\& =\nu (T_{\mu\rightarrow \nu}(A^r)) \\& \leq \nu((T_{\mu\rightarrow \nu}(A))^r),
\end{align*}
$$

by $1$-Lipschitzness of $T_{\mu\rightarrow \nu}.$ In other words, we may transport concentration properties along 1-Lipschitz maps. With this in mind, the following theorem is especially useful:

**Theorem 5:** (Caffarelli's Log-Concave Perturbation Theorem) Let $\mu$ have density $d\mu=\exp(-V)$ and $\nu$ have density $d\nu=\exp(-W)$ such that $\nabla^2 V \lesssim \beta_V I$ and $0 \lesssim \alpha_W I \lesssim \nabla^2 W$, where $\alpha_W$ and $\beta_V$ are positive constants. Then the optimal transport map $T_{\mu\rightarrow \nu}$ is $\sqrt{\beta_V/\alpha_W}$-Lipschitz.

(Interestingly, three recent proofs of this using entropy-regularized optimal transport)

**Corollary:** (Concentration for Strongly Log-Concave Measures) Let $\nu\in\mathcal{P}_2(\mathbb{R}^d)$ have density $d\nu=\exp(-W)$ with $W:\mathbb{R}^d\rightarrow \mathbb{R}$ a $\kappa$-strongly log-concave for $\kappa>0$. Then $\nu(f>m_f+r+r_0)\leq e^{-\frac{r^2}{\kappa}}$.

*Proof:* Let $\gamma_\kappa$ be a standard $d$-dimensional Gaussian with variance $2\kappa^2$. Then by applying Theorem 4 and scaling appropriately, $\gamma_\kappa$ satisfies $T_2(\kappa)$, and hence has the above concentration profile by Theorem 3. By Theorem 5, the optimal transport map $T_{\mu\rightarrow \nu}$ is $1$-Lipschitz, so we may transport this concentration profile to $\nu$.
