---
layout: post
title:  "World-Systems Theory in Data: Centrality and Similarity"
short: "Centrality and Similarity"
date:   2021-10-11 03:00:00 -0800
homepage: /stoclust/worldsys/
categories: stoclust worldsys 
excerpt: "I use relative entropy to cluster nations into central and peripheral zones."
visible: 0
---
{% newthought '**Tl;dr:**' %} The package `stoclust` can be applied to 
global trade networks, for the purpose of hierarchically
clustering nations based on similarity in their trade relations. Clusters with high
centrality tend to have high internal cohesion, as predicted by world-systems
theory. In the following interactive diagram, the reader can explore the
clusters at various scales. Read further for more explanation and interactive diagrams.

{% marginfigure 
'mf-wallerstein' 'assets/img/wallerstein.png' 'A visual schematic of
the world-systems model of global trade. Reproduced from Wikimedia Commons.'  %}

{% newthought 'This post and its sequel' %} will showcase some uses of `stoclust` in an examination
of global trade. We will be examining the primary hypotheses of *world-systems
theory*. The first of these is that the global trade network sorts nations on an axis of
centrality/peripherality, where central (or *core*) nations have strong trade relations with
other core nations, and peripheral nations' trade relations are also
dominated by core nations. The second hypothesis is that the division between
core and periphery correlates to an international division of labor, where core
nations tend to export manufactured and peripheral nations tend to
export labor-intensive and raw materials. 

{% marginnote 
'plug' 'I will note that one way of examining these hypotheses would be to compute some network
measure of centrality for each country, and also compute whether that country
tends to export or import embodied labor (and other resources) 
through an input-ouptut analysis.
However, our recent paper demonstrates that the intrinsic structure of
input-output models will bias results in favor of world-systems theory and so
this is not a suitable approach.' %}

We will examine these hypotheses in two separate
posts. The first (and current) post will come up with a clustering scheme that
groups countries simultaneously by their centrality and similarity in trade
relations. The second will perform another clustering, this time based on export
types, and examine if the two clustering schemes are correlated.

{% newthought 'Core-periphery networks' %} are defined by two groups of nodes---a *core* and a
*periphery*---with core nodes having dense relations with one another and
peripheral nodes mostly having connections with core nodes.

For cases where the network consists of weighted edges---as is the case in a trade network dataset,
where the weights might be the total dollar value of shipments between two
nations---a number of methods have been developed, usually around the principle
of block-modeling, to divide networks into cores and peripheries. My
demonstration is going to use a tool from information theory, *relative
entropy*, to cluster countries with the aid of the package `stoclust.`

{% newthought 'Relative entropy originates' %} in the area of hypothesis
testing. Simply put, suppose you are shown $$N$$ samples from an unknown probability
distribution $$\mathbf{p}$$. The chance of confusing the samples with another
distribution $$\mathbf{q}$$ is proportional to

$$
p_{\mathrm{confusion}} \sim e^{-ND(\mathbf{p}\|\mathbf{q})}
$$

where $$D(\mathbf{p}\|\mathbf{q})$$ is the relative entropy, given by

$$
D(\mathbf{p}\|\mathbf{q}) = \sum_i p_i \log \frac{p_i}{q_i} 
$$

We will consider a form of relative entropy modified for our trade scenario. Let
$$V_{ij}$$ be the value of sales from nation $$i$$ to nation $$j$$. We're
going to normalize this into a set of probability distributions, called
$$T_{ij}$$:

$$
T_{ij} = \frac{V_{ij}}{\sum_j V_{ij}}
$$

This gives the distribution of nations $$j$$ which import $$i$$'s products. For
each $$i$$, $$\mathbf{T}_i = T_{ij}$$ is a probability distribution over $j$.

Now let's define the *cross-entropy* $$D_{ij}$$ between two nations
$$i$$ and $$j$$ as the quantity

$$
D(i\|j) = \sum_{k\neq i,j} T_{ik} \log \frac{T_{ik}}{T_{jk}} + T_{ii} \log
\frac{T_{ii}}{T_{jj}} + T_{ij} \log \frac{T_{ij}}{T_{ji}}
$$

Imagine a game where you are shown the sales tables for an unknown country. You
might easily guess the nation by the fact that it probably sells more to itself
than any other country. However, suppose we modify the game. The unknown country
$$i$$ and an alternative $$j$$ are simply relabeled as "Self" and "Alternative"
on the list. You must now guess between $$i$$ and $$j$$ based only on trade with other
(non-$$i,j$$) nations, and the balance of trade between $$i$$ and $$j$$. The
cross-entropy describes the difficulty of confusing $$i$$ and $$j$$ in this
game.

{% newthought We used the Global Trade Aggregation Project%}, or GTAP, to
acquire trade data for 134 regions around the world. We computed the
cross-entropy between these regions. I'll skip over the data collection code: I
have a repository where you can learn more about that. 

