class: middle, center, title-slide
count: false

# Likelihood preservation and statistical reproduction of searches for new physics
<br>

Matthew Feickert<br>
[matthew.feickert@cern.ch](mailto:matthew.feickert@cern.ch)

[CHEP 2019](https://indico.cern.ch/event/773049/contributions/3476143/)

November 7th, 2019

---
# Summary of Invited Talk Information and Guidelines

Form the CHEP page on [Instructions to speakers](https://indico.cern.ch/event/773049/page/17867-instructions-to-speakers)

- Topic: [Likelihood preservation and statistical reproduction of searches for new physics](https://indico.cern.ch/event/773049/contributions/3476143/)
   - [ATL-PHYS-PUB-2019-029](https://cds.cern.ch/record/2684863)
- ATLAS Talk?: Yes
- Time Limit: 15 minutes (All parallel session talks are .blue[12 minutes] + **3 minutes** for questions)
- Slides must be prepared for projection 16:9 format (longer side along the horizontal direction) ✓

---
# Collaborators

<br><br>

.grid[
.kol-1-3.center[
.circle.width-80[![Lukas](figures/collaborators/heinrich.jpg)]

[Lukas Heinrich](https://github.com/lukasheinrich)

CERN
]
.kol-1-3.center[
.circle.width-80[![Giordon](https://avatars0.githubusercontent.com/u/761483)]

[Giordon Stark](https://github.com/kratsg)

UCSC SCIPP
]
.kol-1-3.center[
.circle.width-70[![Kyle](figures/collaborators/cranmer.png)]

[Kyle Cranmer](http://theoryandpractice.org/)

NYU
]
]

---
# Likelihood serialization...

.center[...making good on [19 year old agreement to publish likelihoods](https://indico.cern.ch/event/746178/contributions/3396797/)]

<br>

.center.width-100[
[![likelihood_publishing_agreement](figures/likelihood_publishing_agreement.png)](https://cds.cern.ch/record/411537)
]

.center[([1st Workshop on Confidence Limits, CERN, 2000](http://inspirehep.net/record/534129))]

<br>

.center[Problem: How to communicate multidimensional likelihoods?]

---
# HistFactory

<br>

- A flexible p.d.f. template to build statistical models from binned distributions and data
- Developed by Cranmer, Lewis, Moneta, Shibata, and Verkerke [1]
- Widely used by the HEP community for standard model measurements and BSM searches
   <!-- - Show public summary plots and link to references that use HistFactory (multi b-jets for example) -->

.kol-1-1.center[
.width-100[![HistFactory_uses](figures/HistFactory_result_examples.png)]
]

---
# HistFactory Template

<br>

$$\begin{aligned}
&\mathcal{P}\left(n\_{c}, x\_{e}, a\_{p} \middle|\phi\_{p}, \alpha\_{p}, \gamma\_{b} \right) = \\\\
&{\color{blue}{\prod\_{c \\,\in\\, \textrm{channels}} \left[\textrm{Pois}\left(n\_{c} \middle| \nu\_{c}\right) \prod\_{e=1}^{n\_{c}} f\_{c}\left(x\_{e} \middle| \vec{\alpha}\right)\right]}} {\color{red}{G\left(L\_{0} \middle| \lambda, \Delta\_{L}\right) \prod\_{p\\, \in\\, \mathbb{S}+\Gamma} f\_{p}\left(a\_{p} \middle| \alpha\_{p}\right)}}
\end{aligned}$$

.bold[Use:] Multiple disjoint _channels_ (or regions) of binned distributions with multiple _samples_ contributing to each with additional (possibly shared) systematics between sample estimates

.bold[Main pieces:]

- .blue[Main Poisson p.d.f. for bins observed in all channels]
- .red[Constraint p.d.f. (+ data) for "auxiliary measurements"]
   - encoding systematic uncertainties (normalization, shape, etc)

---
# HistFactory Template pyhf

$$
f\left(n, a\middle|\eta, \chi\right) = \color{blue}{\prod\_{c \\,\in\\, \textrm{channels}} \prod\_{b \\,\in\\, \textrm{bins}\_c} \textrm{Pois} \left(n\_{cb} \middle| \nu\_{cb}\left(\eta,\chi\right)\right)} \color{red}{\prod\_{\chi \\,\in\\, \chi} c\_{\chi} \left(a\_{\chi}\middle|\chi\right)}
$$

<!-- $$\begin{aligned}
\nu\_{cb}(\phi) &= \sum\_{s \\,\in\\, \textrm{samples}} \nu\_{scb}(\nu, \chi)\\\\
&= \sum\_{s \\,\in\\, \textrm{samples}} \underbrace{\left(\sum\_{\kappa \\,\in\\, \kappa} \kappa\_{scb}(\nu, \chi)\right)}\_{\textrm{multiplicative}} \Bigg(\nu\_{scb}^{0}(\nu, \chi) + \underbrace{\sum\_{\Delta \\,\in\\, \Delta} \Delta\_{scb}(\nu, \chi)}\_{\textrm{additive}}\Bigg)
\end{aligned}$$ -->
$$
\nu\_{cb}(\nu, \chi) = \sum\_{s \\,\in\\, \textrm{samples}} \underbrace{\left(\sum\_{\kappa \\,\in\\, \kappa} \kappa\_{scb}(\nu, \chi)\right)}\_{\textrm{multiplicative}} \Bigg(\nu\_{scb}^{0}(\nu, \chi) + \underbrace{\sum\_{\Delta \\,\in\\, \Delta} \Delta\_{scb}(\nu, \chi)}\_{\textrm{additive}}\Bigg)
$$

.bold[Use:] Multiple disjoint _channels_ (or regions) of binned distributions with multiple _samples_ contributing to each with additional (possibly shared) systematics between sample estimates

.bold[Main pieces:]
- .blue[Main Poisson p.d.f. for simultaneous measurement of multiple channels]
- .red[Constraint p.d.f. (+ data) for "auxiliary measurements"]
   - encoding systematic uncertainties (normalization, shape, etc)
- .katex[Event rates] $\nu\_{cb}$ from nominal rate $\nu\_{scb}^{0}$ and rate modifiers $\kappa$ and $\Delta$

---
# Formation definition

Following Hopcroft and Ullman (1979, p. 148), a (one-tape) Turing machine can be formally defined as a 7-tuple $M=(Q,\Gamma,b,\Sigma,\delta, q\_0, F)$, where
- $Q$ is a finite, non-empty set of states;
- $\Gamma$ is a finite, non-empty set of tapes alphabet symbols;
- $b \in \Gamma \setminus \\{b\\}$ is the set of input symbols, that is, the set of symbols allowed to appear in the initial tape contents;
- $q\_0 \in Q$ is the initial state;
- $F \subseteq Q$ is the set of final states or accepting states. The initial tape contents is said to be accepted by $M$ if it eventually halts in a state from $F$.
- $\delta: (Q \setminus F) \times \Gamma \rightarrow Q \times \Gamma \times \\{L,R\\}$ is the state transition function.

---

Next slide

.footnote[This is a footnote.]

---

class: middle

# Summary

---

class: middle

- abc
- def
- ghi

---
class: end-slide, center

Backup


---
# References

1. ROOT collaboration, K. Cranmer, G. Lewis, L. Moneta, A. Shibata and W. Verkerke, .italic[[HistFactory: A tool for creating statistical models for use with RooFit and RooStats](http://inspirehep.net/record/1236448)], 2012.
2. L. Heinrich, H. Schulz, J. Turner and Y. Zhou, .italic[[Constraining $A_{4}$ Leptonic Flavour Model Parameters at Colliders and Beyond](https://inspirehep.net/record/1698425)], 2018.

---

class: end-slide, center
count: false

The end.
