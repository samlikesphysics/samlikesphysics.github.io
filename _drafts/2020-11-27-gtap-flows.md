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

This post and its sequel will showcase some uses of stoclust in an examination
of global trade. We will be examining the primary hypotheses of *world-systems
theory*. The first of these is that the global trade network sorts nations on an axis of
centrality/peripherality, where central (or *core*) nations have strong trade relations with
other core nations, and peripheral nations' trade relations are also
dominated by core nations. The second hypothesis is that the division between
core and periphery correlates to an international division of labor, where core
nations tend to export capital-intensive goods and peripheral nations tend to
export labor-intensive goods. 

We will examine these hypotheses in two separate
posts. The first (and current) post will come up with a clustering scheme that
groups countries simultaneously by their centrality and similarity in trade
relations. The second will perform another clustering, this time based on export
types, and examine if the two clustering schemes are correlated.{% sidenote 
'plug' 'I will note that one way of examining this would be to compute some network
measure of centrality for each country, and also compute whether that country
tends to export or import embodied labor through an input-ouptut analysis.
However, our recent paper demonstrates that the intrinsic structure of
input-output models will bias results in favor of world-systems theory and so
this is not a suitable approach.' %}