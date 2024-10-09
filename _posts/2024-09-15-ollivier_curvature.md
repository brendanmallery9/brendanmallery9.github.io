---
layout: distill
title: Transport Inequalities
description: an example of a distill-style blog post and main elements
tags: distill formatting
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

  There is a very rich connection between convexity and notions of curvature for Markov processes, which has given rise to a number of fruitful analogies. As far as I can tell, these analogies all arise from the following idea: Just as (strict) convexity is often just the right condition to guarantee (fast) convergence of a gradient flow to a minima, (positive) curvature for a Markov process is the right condition to guarantee (fast) convergence of a Markov process to equilibrium. What's more, these conditions also ensure uniqueness of the limiting object for these dynamical systems. In this post, we will outline an elementary instance of this connection for the notion of Ollivier Ricci curvature.

  ## Convexity

  Recall that a function $f:\mathbb{R}^d\rightarrow \mathbb{R}$ is $\alpha$-strictly convex (for $\alpha\geq 0$) if it satisfies the following inequality: 

  $$f(x)-f(y)\geq \langle \nabla f(y),x-y\rangle +\frac{\alpha}{2}||y-x||^2$$

  for all $x$ and $y$. Observe that a $0$-strictly convex function is simply a convex function. Strict convexity is a strong condition for a function to satisfy, and has a number of important consequences. From an optimization perspective, the two that stand out are:

  1. Strictly convex functions have a unique minimum, and;

  2. It is easy to find this minimum by following the gradient.

  The first property is trivial to verify: Observe that if there were two minima $x_1^*$ and $x_2^*$, the above inequality reduces to 
  $$0\geq \langle \nabla f(x_1^*),x_1^*-x_2^*\rangle +\frac{\alpha}{2}||x_1^*-x_2^*||^2$$

  and since $\nabla f(x_1^*)=0$ we have $x_1^*=x_2^*$. The second property can be proved in both discrete and continuous time, where in the first case, "following the gradient" means gradient descent, i.e. setting $x_t=x_{t-1}-\eta\nabla f(x_{t-1})$ for some initialization $x_0$ and stepsize $\eta>0$. The continuous time analog is gradient flow, which is defined by the differential equation 
  $$\dot{x}_t=-\nabla f(x_t),$$

  with some initial condition $x_0$. The discrete case is more relevant for this analogy, so we give the standard proof here. For convenience we assume $f$ is L-Lipschitz, in which case we can set $\eta=\frac{1}{L}$. Let $x_0\in \mathbb{R}^d$, and let $x_*=\min_{y\in \mathbb{R}^d} f(y)$. Then: 

  $$||x_{t+1}-x_*||^2_2 = ||x_t-x_*-\eta \nabla f(x_t)||^2_2 $$ $$=||x_t-x_*||^2_2-2\eta\langle \nabla f(x_t),x_t-x_*\rangle +\eta^2 ||\nabla f(x_t)||^2_2$$

  By $\alpha$-strong convexity and $L$-smoothness, we may upper bound this by 

  $$\leq (1-\eta \alpha)||x_t-x_*||^2_2-2\eta(f(x_t)-f(x_*))+2\eta^2 L(f(x_t)-f(x_*))$$

  $$=(1-\eta \alpha)||x_t-x_*||_2^2-2\alpha(1-\alpha L) (f(x_t)-f(x_*))$$ $$=(1-\eta\alpha)||x_t-x_*||^2_2$$

  Iterating this, we get that: 
  
  $$||x_t-x_*||_2^2\leq (1-\eta\alpha)^t||x_0-x_*||_2^2$$

  which implies that $x_t$ converges to the solution in $||.||_2^2$ exponentially fast. We make two remarks:
  1. If we remove the smoothness assumption from $f$, one may still conclude that (a suitably generalized version of) gradient descent will converge provided one appropriately shrinks the step-size at each iteration (otherwise one is left with an error proportional to $\eta$).
  2. The same proof holds for all $0\leq \eta \leq \frac{1}{L}$.

  The first part to our analogy is that the exponential rate of convergence is governed by the strength of convexity $\alpha$: if we ignore $\eta$ by setting it equal to $1$ (hence assuming that $f$ is 1-Lipschitz), then we can consider $\mathbb{R}^d$ under the dynamical system defined by mapping $$T:\mathbb{R}^d\rightarrow \mathbb{R}^d$$$$T(x) =x-\nabla f(x).$$
  for $f$ an $\alpha$-strongly convex function. Then $T^t$ contracts $\mathbb{R}^d$ by a factor of $(1-\alpha)^t$. Thus we may view $\alpha$ as the coefficient of contraction for the self map of $\mathbb{R}^d$ induced by the (discrete) gradient flow of $f$. Over many applications of the map, the entire metric space contracts to a point $x_*$ which is the minima for $f$. This also constitutes a proof of the uniqueness of the minimal value for $f$.

  ## Ricci Curvature

  **Definition:** (Ollivier Ricci Curvature) Ollivier Ricci curvature, which is a notion of curvature that is defined for a Markov chain on a metric space $X$. Let $M:x\rightarrow \mathcal{P}(X)$ be Markov kernel, i.e. a measurable map from $X$ to $\mathcal{P}(X)$, the set of probability measures on $X$. Then the Ollivier Ricci curvature of $M$ is:

  $$\kappa(x,y)=\frac{d(x,y)-W_1(M(x),M(y))}{d(x,y)}.$$

  where $d$ is the metric on $X$ and $W_1$ is the 1-Wasserstein, or optimal transport distance on $\mathcal{P}(X)$. 

  How should one think about this curvature? It is most natural to think about $M(x)$ as a probability measure centered at $x$ (for instance the uniform measure on a ball centered with $x$ at its center). Then one can think of $M$ as defining a density of particles around each point in the metric space. Then $\kappa(x,y)$ can be seen as a comparison between the distance a particle at $x$ must travel to reach $y$ versus the "average" distance a particle nearby $x$ must travel to reach a particle nearby $y$. If $\kappa(x,y)\geq 0$, then a random nearby particle must on average travel less distance than the one placed at $x$, whereas if $\kappa(x,y)\leq 0$, the nearby particle must travel further. Thus $\kappa(x,y)$ says something about the "local geometry" of the pair of points $(x,y)$. 

  The easiest way to convince yourself that this is a good notion of curvature is by example. For the following examples, we take $M$ to be the uniform measure on a ball of some radius $r>0$ around each point in $X$:
  - The quintessential positively curved space, a sphere, has everywhere positive Ollivier Ricci curvature. This is easiest to see when $x$ and $y$ are antipodal points on the sphere. In this case, $M(x)$ and $M(y)$ are small "caps" on the ends of the sphere, and one should have no problem believing that $W_1(M(x),M(y))<d(x,y)$. 
  - "Tree-like" metric spaces tend to have negative curvature. Let $\mathcal{T}$ infinite tree with minimum degree at least $3$, equipped with the graph metric. Let $x$ and $y$ be two points which are separated by at least 3 edges. Then one can easily compute that the distance between $x$ and $y$ is less than the average distance between a point in the support of $M(x)$ and the support of $M(y)$. If one is familiar with $\delta$-hyperbolicity, or the fact that an infinite tree embeds quasi-isometrically into hyperbolic space, one will be satisfied with the definition in this case.
  - The natural example of a flat space is Euclidean space. As we have already mentioned in the case of $\mathbb{R}^2$, $W_1(M(x),M(y))=d(x,y)$ for two balls $M(x)$ and $M(y)$, centered at $x$ and $y$ respectively, hence $\kappa(x,y)=0$. 

  In all of the above, the dependence on a Markov chain is avoided to highlight the geometric nature of $\kappa$. But our main interest in $\kappa$ comes from the following theorem, which equates positive curvature of $M$ with rapid convergence of the Markov process generated by $M$: For any Markov kernel $M$ and probability measure $\mu$, we denote $M*\mu$ as the convolution of $\mu$ by $M$. 
  **Theorem** Let $(X,d)$ be a metric space and $M$ a Markov kernel on $X$. Then $\kappa(x,y)>K>0$ for all $x,y\in X$ iff $W_1(M*\mu,M*\nu)\leq (1-\alpha)W_1(\mu,\nu)$ for all $\mu,\nu\in \mathcal{P}(X)$.

  The theorem was first discovered (as far as I can tell) in the context of path coupling by [Bubbly and Dyer](https://www.math.cmu.edu/~af1p/Teaching/Markov_Chain_Mixing/Papers/Pathcouple.pdf), and hence predates the definition of $\kappa$. To rephrase it in a way more suggestive in our analogy, convolution by $M$ defines a map 
  $$M*:\mathcal{P}(X)\rightarrow \mathcal{P}(X)$$

  sending $\mu$ to $M*\mu$. Then if $(M*)^t$ has curvature bounded below by $\alpha>0$, $M*$ is a contraction, and in particular contracts $(\mathcal{P}(\Omega),W_1)$ by a factor of $(1-\alpha)^t$. Over many applications of $M*$, the entire space $\mathcal{P}(\Omega)$ contracts to the stationary distribution of $M*$, which is necessarily unique. 

  **Convexity meets curvature**

  We've seen that both $\alpha$-convexity for a function $f$ and $\kappa>\alpha$ for a Markov kernel imply contraction properties for dynamical systems associated to these objects. These two properties come together in a very nice way when considering Langevin diffusion. Langevin diffusion is a stochastic process on $\mathbb{R}^d$, governed by the following stochastic differential equation:
  $$dX_t=-\nabla V(X_t)dt+dB_t$$

  where $V:\mathbb{R}^d\rightarrow\mathbb{R}$ is a potential function and $B_t$ is a standard Brownian motion. One can think of $X_t$ as the trajectory of a particle undergoing random motion in a force field $\nabla V$. As $t\rightarrow \infty$, the law of $X_t$ converges to a unique stationary distribution, given by the Gibbs measure $\mu_*= \frac{1}{Z}e^{-V}$, with the normalizing constant $Z=\int_{\mathbb{R}^d} e^{-\nabla V(x)}dx$. The rate at which the process converges to its stationary distribution is a well-studied topic, as it suggests natural sampling schemes for distributions that can be written in the form $\frac{1}{Z}e^{-V}$. In particular, if one assumes that $V$ is $\alpha$-strongly convex, one is guaranteed exponential convergence of the Langevin diffusion to $\mu_*$. This can be proved directly in a fairly straightforward manner, but we will take a nonstandard perspective on this, which was first made clear to me by the aforementioned blog post.

  Consider the Euler-Marayama discretization of $X_t$, with $k+1$'st iterate:
  $$x^{k+1}=x^{k}-\frac{\delta}{2}\nabla V(x^k) + \sqrt{\delta}\zeta$$

  for $\zeta$ distributed according to a standard normal $\mathcal{N}(0,1)$ and $\delta>0$. This gives rise to a Markov chain, and so we may try to compute its Ollivier Ricci curvature. Let $x_0,y_0$ be two different initial points in $\mathbb{R}^d$, and let $M(x)=\mu_1^x$ and $M(y)=\mu_1^y$ be the laws of $x_1$ and $y_1$ respectively. Then we have:

  $$\mu_1^x=\mathcal{N}(x_0,\delta)*\delta_{x_0-\frac{\delta}{2}\nabla V(x_0)}$$ $$\mu_1^y=\mathcal{N}(y_0,\delta)*\delta_{y_0-\frac{\delta}{2}\nabla V(y_0)}$$

  We may couple these two measures by pushing $\mu_1^x$ forward onto $\mu_1^y$ by translation by the vector $y_0-\frac{\delta}{2}\nabla V(y_0)-(x_0-\frac{\delta}{2}\nabla V(x_0))\in \mathbb{R}^d$, and hence we may upper bound $W_1(\mu_1^x,\mu^y_1)$ as follows:

  $$W_1(\mu_1^x,\mu_1^y)\leq ||x_0-y_0-\frac{\delta}{2}(\nabla V(x_0)-\nabla V(y_0))||$$ 

  $$= ||x_0-y_0||\left(1-\frac{\delta}{2}\frac{\nabla V(x_0)-\nabla V(y_0)}{||x_0-y_0||}\right)||$$

  If we now assume that $V$ is $\alpha$-strongly convex, we may upper bound this quantity by: 

  $$||(x_0-y_0)\left(1-\frac{\delta}{2}\alpha\right)||$$

  Plugging this bound into our formula for the curvature between $x_0$ and $y_0$, we have: 
  $$\kappa(x_0,y_0)\geq \frac{||x_0-y_0||-||(x_0-y_0)(1-\frac{\delta}{2}\alpha)||}{||x_0-y_0||}$$

  $$\geq \frac{\delta}{2}\alpha.$$

  As this is true for all initial points $x_0,y_0$, we have a global positive curvature bound of $\frac{\delta\alpha}{2}$, which guarantees that the Euler-Marayama discretization of $X_t$ converges to equilibrium at a rate of at least $(1-\frac{\delta}{2}\alpha)^t$. Thus we see that the convexity of $V$ directly implies a positive curvature bound for (a discrete approximation to) the Langevin diffusion with potential $V$, and together they imply an exponential rate of convergence for this process. 

  **Concluding remarks**

  As I mentioned previously, proving the continuum analog of the above result is not very difficult, but its worth noting that the two arguments are essentially identical in spirit. The key to both is coupling two independent copies of the process initialized at different points, and then concluding by a curvature bound (in the discrete case) or Gronwall's inequality (in the continuum case). 

  Nevertheless, one could imagine trying to use the discrete time result to prove convergence of the continuous Langevin diffusion. We sketch out one idea: It can be shown that a positive curvature bound for a Markov chain implies a spectral lower bound on the associated Markov operator (via Kantorovich duality). The Euler-Marayama discretization converges (in several senses) to $X_t$ as $\delta\rightarrow 0$, so it is reasonable to think that the generator of the continuous process is well approximated by these Markov operators for small $\delta$. As uniform Wasserstein bounds are very robust under these kinds of limiting operations, its likely one could obtain a spectral lower bound, or at least something equally useful on the generator, from which one could extract a rate of convergence for the process.