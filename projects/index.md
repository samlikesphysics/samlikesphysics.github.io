---
layout: page
title: Projects
---
This page contains some summaries of the projects I've worked on. Click the link
in the list below to be taken to the project summary.

{% newthought Contents %}

+ [`ruckus`](#ruckus)  
+ [Carbon Chaos!](#CarbonChaos)
+ [Efficient Quantum Computing](#QuantumCompression) 
+ [`stoclust`](#stoclust) 

<hr class="slender">
## `ruckus`<a name="stoclust"></a>
#### Kernel embedding networks with Python and `scikit-learn`

`ruckus` is my latest project---a Python package for working with networks of reproducing
kernel Hilbert spaces, for use in machine learning, time-series analysis, 
and dynamical systems modeling. This package is inspired by and intended to further my own work
on the foundations of RKHS methods for time-series prediction [(Loomis & Crutchfield
2021)](https://arxiv.org/abs/2109.09203).

Reproducing kernel Hilbert spaces (RKHS’s, or, as I say it, “ruckuses”) form the mathematical bedrock of numerous machine learning techniques, from support vector machines and Gaussian processes to neural tangent kernels and random feature embeddings.

`ruckus` provides specialized objects for defining, fitting and applying RKHS's to data,
as well as the necessary tools to build intricately-designed deep and convolutional RKHS networks.
It also supports kernel distributional embeddings and efficient sampling of forecasts via kernel herding. 

{% maincolumn 'assets/img/Lorenz.png' 
'Predicting the Lorenz attractor with `ruckus`: see our
[example](https://samlikesphysics.github.io/ruckus/#example) in the documentation.' %}

*This project is a work in progress. Stay tuned for more updates!*

{% newthought Packages %}

#### [`ruckus`](https://samlikesphysics.github.io/ruckus/)

+ [Return to top](/projects/)

<hr class="slender">
## Carbon Chaos!<a name="CarbonChaos"></a>
#### Nonequilibrium Methods in Emissions Analysis

{% newthought 'The "carbon footprint"' %} has become a fairly ubiquitous character in discussions
of climate change and economic policy. The methods for computing footprints
originate in the field of *input-output analysis*, which traces through networks
of economic dependency to link up consumption activities with the production
activities---and resulting emissions---which sustain them. This allows not only
calculating how much carbon is necessary to support someone's lifestyle, but
also determines the geographic distribution of emissions, linking up the consumption practices
of one region with pollution in another.

{% maincolumn_html 'assets/html/co2con_net.html' 'This interactive figure shows
the network of "carbon dependencies" across the globe. Hover over a node to see
the region. An arrow pointing from, say, "South America" to "Europe" indicates
that emissions produced in South America are a part of the European carbon
footprint.' 90 550 %}

Input-output analysis rests on a number of assumptions. We analyzed the
consequences of these assumptions in [(Loomis, Cooper & Crutchfield
2021)](https://arxiv.com/abs/2106.03948), with data from the [Global Trade
Aggregation Project](https://www.gtap.agecon.purdue.edu/). 
The upshot is that whether a nation's
footprint is located within domestic borders or beyond is primarily determined
by that nation's "carbon intensity": the amount of $$\mathrm{CO}_2$$ emitted 
per dollar of income. This arises as a theoretical consequence of input-output
assumptions, with *majorization*---a tool from nonequilibrium
thermodynamics---playing a central role. These results give a better
understanding of how input-output models derive their results, but consequently casts doubt
on their ability to properly test hypotheses of *unequal exchange* of embodied
pollution between regions.

{% maincolumn 'assets/img/carbonmap.png' 
'Map color indicates the measured "carbon intensity" of each region. Leontief analysis
was applied to null models generated with random trade networks; pie wedges
indicate the probability of being a net exporter vs. importer of embodied
carbon. High-intensity
regions had a strong tendency to export embodied carbon, 
even when economic structure was completely randomized. This can be explained
with tools from thermodynamics: see 
[(Loomis, Cooper & Crutchfield 2021)](https://arxiv.com/abs/2106.03948).' %}

Because this effect is purely mathematical in nature, it can be observed for any
resource one tracks through input-output analysis. The following graph shows the
relationship between national average wage (the analagous "intensity" for labor)
and the ratio of produced to consumed embodied labor, for each nation. The
correlation is highly suggestive. However, it is chiefly a mathematical effect.
Input-output analysis *predicts* that high-wage nations import more embodied
labor, but it does not *provide evidence*, an important distinction elucidated
by our thermodynamic analysis.

{% maincolumn_html 'assets/html/labcon_wage.html' "The x-axis shows the ratio of
produced to consumed embodied labor by each nation (P/C ratio). The y-axis shows
the national wage. We also include the Kendall-Tau correlation measure for these
two variables: $$\tau = -0.65$$. Hover over a dot to see the nation's ISO
identifier and the precise values of wage and P/C. Nations are color-coded
according to region." 90 550 %}

One of the more questionable assumptions of input-output analysis, which is
crucial to the results above, is its inherent linearity.
Further work in this area will seek to offer alternatives to input-output
analysis, performing nonlinear dynamical analysis of policy impacts to determine
the more complex relationships between consumption, production and emissions.

{% newthought Articles %}

#### [Loomis et al. Nonequilibrium thermodynamics in measuring carbon footprints. Submitted.](https://arxiv.com/abs/2106.03948)

{% newthought Packages %}

#### [github.com/samlikesphysics/netacam_code.git](https://github.com/samlikesphysics/netacam_code)

+ [Return to top](/projects/)

<hr class="slender">
## Efficient Quantum Computing<a name="QuantumCompression"></a>
#### Quantum memory compression and energy savings

{% epigraph 'Computers may be thought of as engines for transforming free energy
into waste heat and mathematical work.' 'Charles Bennett' "The thermodynamics of
computation---a review. 1982." %}

{% newthought 'Einstein proved that matter and energy could be interchanged;' %}
some time later, Rolf Landauer proved that energy and *information* could be
interchanged as well. More specifically, in his resolution of the paradox of
Maxwell's Demon, Landauer demonstrated{% sidenote 'Lan' 
'R. Landauer. *Irreversibility and heat generation in the computing process.* 1961.' %} 
that the erasure of a bit of information
required expending a minimum amount energy, $$kT\ln 2$$.{% sidenote 'kT' 'Here $$k$$
is the Boltzmann constant and $$T$$ is the ambient temperature of the computer.'
%}
Bit erasure is a key tool in computational tasks and so Landauer's
principle placed fundamental energy costs on computation itself.

We've contributed to this line of work by studying a particular computational
task: simulating a specified pattern, written onto an empty tape. Though this
may sound simple, the pattern may be arbitrarily complicated: anything from
random data to Shakespeare. This makes simulation an extremely deep arena for
studying the costs of computation.

The most efficient machine for generating a pattern using only classical physics is
called an $$\epsilon$$-machine. We examined a recent quantum extension of the
$$\epsilon$$-machine, called the $$q$$-machine, and put it to the test: under
what conditions do $$q$$-machines provide crucial advantages in memory and
energy costs?

{% maincolumn 'assets/img/quantum3.png' 
'A schematic of a computer which writes a specified pattern of symbols onto
an empty tape. The computer is governed by a stochastic controller called the 
$$\epsilon$$-machine. It may utilize both heat and free energy to alter the
tape, and it has a finite set of memory states for reference. From [(Loomis &
Crutchfield 2020)](https://doi.org/10.1103/physrevlett.125.020601).' %}

We provided the first proofs that $$q$$-machines are *always* able to improve on
$$\epsilon$$-machines in memory costs 
[(Loomis & Crutchfield 2019)](https://doi.org/10.1007/s10955-019-02344-x).
However, this work did not initially address the thermodynamic angle, so it
remained unclear whether this improvement in memory came at a cost. The answer
required distinguishing between two classes of $$\epsilon$$-machine, called the
*forward* and *reverse* varieties. We discovered in two companion papers{%
sidenote 'Pprs' '[Thermal efficiency of quantum memory
compression](https://doi.org/10.1103/physrevlett.125.020601) and
[Thermodynamically efficient local
computation](https://doi.org/10.1103/physrevresearch.2.023039)'%}
that while forward $$\epsilon$$-machines are less efficient both in memory and
energy costs, reverse $$\epsilon$$-machines exhibit a tradeoff: they leverage
their additional memory costs to save on energy costs. Vice-versa, quantum
$$q$$-machines exhibit higher energy costs in order to save on memory.

{% maincolumn 'assets/img/quantum1.png' 
'In a heuristic plot of memory vs. energy efficiency, we show that while both
forward and reverse $$\epsilon$$-machines require higher memory overhead than
the $$q$$-machines, only the reverse $$\epsilon$$-machines achieve maximum
energy efficiency.
From [(Loomis & Crutchfield 2020)](https://doi.org/10.1103/physrevresearch.2.023039).' %}

**Takeaway: Quantum can save space and time---but when it comes to generating
patterns, classical is still the most energy-efficient way to go.**

{% newthought Publications %}

#### [Loomis & Crutchfield. Thermodynamically efficient local computation. 2020](https://doi.org/10.1103/physrevresearch.2.023039)
#### [Loomis & Crutchfield. Thermal efficiency of quantum memory compression. 2020](https://doi.org/10.1103/physrevlett.125.020601)
#### [Loomis et al. Optimizing quantum models of classical channels. 2020](https://doi.org/10.1007/s10955-020-02649-2)
#### [Loomis & Crutchfield. Strong and weak optimizations in classical and quantum models of stochastic processes. 2019](https://doi.org/10.1007/s10955-019-02344-x)
#### [Aghamohammadi et al. Extreme quantum memory advantage for rare-event sampling. 2018](https://doi.org/10.1103/physrevx.8.011025)

+ [Return to top](/projects/)

<hr class="slender">
## `stoclust`<a name="stoclust"></a>
#### Stochastic clustering in Python

`stoclust` is a package of modularized methods for stochastic and ensemble
clustering techniques. By modular, I mean that there are few methods in this
package which act as a single pipeline for clustering a dataset–––rather, the
methods each form a unit of what might be a larger clustering routine.

These modular units are designed to be compatible with general clustering
methods from other packages, like `scipy.clustering` or `sklearn.cluster`. However,
we also provide specific methods for implementing clustering algorithms whose
underlying mathematics is rooted in stochastic analysis and dynamics.
Additionally, one can add a stochastic twist to any clustering method by using
ensemble clustering, which uses randomness to probe the stability and robustness
of clustering results.

{% newthought Packages %}

#### [`stoclust`](https://samlikesphysics.github.io/stoclust/)

+ [Return to top](/projects/)

<hr class="slender">
{% newthought " *Rome wasn't built in a day.* " %} *And that would be crazy, because
this website is far less complicated and also wasn't built in a day. I'll add
more project details soon.*