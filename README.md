# [Likelihood preservation and statistical reproduction of searches for new physics](https://indico.cern.ch/event/773049/contributions/3476143/)

Talk given at the [24th International Conference on Computing in High Energy & Nuclear Physics](https://indico.cern.ch/event/773049/)

Viewable online [here](https://matthewfeickert.github.io/talk-CHEP-2019/index.html?p=talk.md)

## Abstract

Likelihoods associated with statistical fits in searches for new physics are beginning to be published by LHC experiments on HEPData [[arXiv:1704.05473](https://arxiv.org/abs/1704.05473)]. The first of these is the search for bottom-squark pair production by ATLAS [[ATLAS-CONF-2019-011](http://inspirehep.net/record/1727313)]. These likelihoods adhere to a specification first defined by the `HistFactory` p.d.f. template [[CERN-OPEN-2012-016](https://cds.cern.ch/record/1456844)]. This is per-se independent of its implementation in `ROOT` and it is useful to be able to run statistical analysis outside of the `ROOT` and `RooStats`/`RooFit` framework. We introduce a JSON schema that fully describes the `HistFactory` statistical model and is sufficient to reproduce key results from published ATLAS analyses. Using two independent implementations of the model, one in `ROOT` and one in pure Python, we reproduce the sbottom multi-$b$ limits using the published likelihoods on HEPData underscoring the implementation independence and long-term viability of the archived data.

## Acknowledgments

- [pyhf](https://github.com/diana-hep/pyhf) is developed by [Lukas Heinrich](https://github.com/lukasheinrich), [Matthew Feickert](http://www.matthewfeickert.com/), and [Giordon Stark](https://github.com/kratsg) with advice from [Kyle Cranmer](http://theoryandpractice.org/)
- [Matthew Feickert](http://www.matthewfeickert.com/) is supported in part by IRIS-HEP
