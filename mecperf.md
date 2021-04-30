---
title: "Measurement-driven design and runtime optimization in edge computing: Methodology and tools"
layout: page
---

C. Caiazza, C. Cicconetti, V. Luconi, and A. Vecchio,
"Measurement-driven design and runtime optimization in edge computing: Methodology and tools",
_Computer Networks_ (2021),
doi: [https://doi.org/10.1016/j.comnet.2021.108140](https://doi.org/10.1016/j.comnet.2021.108140),
[BibTeX](bib/mecperf2021.bib)

The paper presents the results obtained in the Fed4Fire+ experiment _Estimating the Mobile Edge Computing Infrastructure Performance_ ([MECPerf](https://www.fed4fire.eu/demo-stories/oc6/mecperf/)) where we have:

1. defined an architecture to enable run-time and offline decision making driven by network-layer performance measurements
2. developed a reference implementation of the measurement agents, collectively called MECPerf, available as open source on [GitHub](https://github.com/MECPerf/MECPerf)
3. collected performance measurements with MECPerf in the NITOS testbed of the Fed4Fire+ infrastructure, available on [Zenodo](https://zenodo.org/record/4647753#.YIui3WYzbKY)

To facilitate access to the data collected, we have also implemented a Python library, on [GitHub](https://github.com/MECPerf/MECPerf_NetworkTrace), which can be integrated with other simulation/emulation to obtain (more) realistic performance, in terms of the network-layer dynamics at the edge.

