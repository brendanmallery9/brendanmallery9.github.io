---
layout: distill
title: A Proof of the Heisenberg Uncertainty Principle
description:
tags: ["Uncertainty Principles","Harmonic Analysis"]
giscus_comments: true
date: 2025-12-12
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
## Proof of the Uncertainty Principle

**Theorem (Heisenberg Uncertainty Principle).**  
Let $f \in \mathcal{S}(\mathbb{R})$. Then:

$$
\left(\int_{\mathbb{R}} x^2 |f(x)|^2\,dx\right)
\left(\int_{\mathbb{R}} \xi^2 |\hat f(\xi)|^2\,d\xi\right)
\ge
\frac{\|f\|_{L^2}^4}{16\pi^2}.
\tag{H}
$$

Equality is achieved by $f(x) \propto \exp(-x^2/2)$.

---

### Proof

We claim that (H) is equivalent to

$$
\int_{\mathbb{R}} x^2 |f(x)|^2\,dx
\;+\;
\int_{\mathbb{R}} \xi^2 |\hat f(\xi)|^2\,d\xi
\ge
\frac{\|f\|_{L^2}^2}{2}.
\tag{1}
$$

Assume first that $\|f\|_{L^2}=1$. If we set

$$
A := \int_{\mathbb{R}} x^2 |f(x)|^2\,dx,
\qquad
B := \int_{\mathbb{R}} \xi^2 |\hat f(\xi)|^2\,d\xi,
$$

then (1) says $A+B \ge \frac{1}{2}$. Among all $A,B>0$ with $A+B=C$, the product $AB$ is maximized at $A=B=C/2$; in particular the best universal lower bound on $AB$ given a lower bound on $A+B$ is obtained in the symmetric case. Thus from $A+B \ge \frac{1}{2}$ we obtain

$$
AB \ge \left(\frac{1}{4}\right)^2 = \frac{1}{16},
$$
i.e. $(H)$ in the normalized case. For general $f$, write 
$f = g * \| f \|_{L^2}$ with $\| g \|_{L^2} = 1$ and apply the normalized inequality to $g$, which yields $(H)$.

---

### Harmonic Oscillator Formulation

Let

$$
H = -\frac{1}{2}\frac{d^2}{dx^2} + \frac{1}{2}x^2
$$

be the harmonic oscillator. For any $f \in \mathcal{S}(\mathbb{R})$,

$$
\begin{aligned}
2\langle Hf,f\rangle
&=
\int_{\mathbb{R}} \left(-f''(x)\right)\overline{f(x)}\,dx
+
\int_{\mathbb{R}} x^2|f(x)|^2\,dx \\
&=
\int_{\mathbb{R}} |f'(x)|^2\,dx
+
\int_{\mathbb{R}} x^2|f(x)|^2\,dx
\qquad \text{(IBP)}\\
&=
\int_{\mathbb{R}} |\widehat{f'}(\xi)|^2\,d\xi
+
\int_{\mathbb{R}} x^2|f(x)|^2\,dx
\qquad \text{(Plancherel)}\\
&=
\int_{\mathbb{R}} \xi^2|\hat f(\xi)|^2\,d\xi
+
\int_{\mathbb{R}} x^2|f(x)|^2\,dx.
\end{aligned}
$$

Therefore (1) is equivalent to the spectral gap estimate

$$
\langle Hf,f\rangle \ge \frac{1}{2}\|f\|_{L^2}^2.
\tag{2}
$$

---

### Creation and Annihilation Operators

We compute

$$
\begin{aligned}
H
&=
-\frac{1}{2}\frac{d^2}{dx^2}
+\frac{1}{2}x^2 \\
&=
\frac{1}{2}\left(x+\frac{d}{dx}\right)\left(x-\frac{d}{dx}\right)
+\frac{1}{2}\left(\frac{d}{dx}x-x\frac{d}{dx}\right).
\end{aligned}
$$

Since

$$
\left(x\frac{d}{dx}-\frac{d}{dx}x\right)f(x)
= xf'(x) - (xf(x))'
= xf'(x) - (xf'(x)+f(x))
= -f(x),
$$

we have $\frac{d}{dx}x - x\frac{d}{dx} = \mathrm{Id}$, and hence

$$
H
=
\frac{1}{2}\left(x+\frac{d}{dx}\right)\left(x-\frac{d}{dx}\right)
+\frac{1}{2}\mathrm{Id}.
$$

Define

$$
a=\frac{1}{\sqrt{2}}\left(x+\frac{d}{dx}\right),
\qquad
a^*=\frac{1}{\sqrt{2}}\left(x-\frac{d}{dx}\right).
$$

Then

$$
H = a^*a + \frac{1}{2}\mathrm{Id}.
$$

Consequently, for any $f$,

$$
\begin{aligned}
\langle Hf,f\rangle
&=
\langle a^*af,f\rangle + \frac{1}{2}\langle f,f\rangle \\
&=
\|af\|_{L^2}^2 + \frac{1}{2}\|f\|_{L^2}^2 \\
&\ge
\frac{1}{2}\|f\|_{L^2}^2,
\end{aligned}
$$

which is exactly (2), and hence proves (1) and (H).

---

### Equality Case

Equality holds if and only if $af=0$, i.e.

$$
\left(x+\frac{d}{dx}\right)f(x)=0.
$$

Equivalently,

$$
f'(x) = -x f(x),
$$

so

$$
f(x)=C\exp\left(-\frac{x^2}{2}\right)
$$

for some constant $C>0$.  
This completes the proof.
