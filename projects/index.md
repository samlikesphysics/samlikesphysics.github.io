---
layout: page
title: Projects
---
This page contains some summaries of the projects I've worked on. For some
sections, the title is a link, and will take you to a page with further details.

## Carbon Chaos!
#### Nonequilibrium Methods in Emissions Analysis
The "carbon footprint" has become a fairly ubiquitous character in discussions
of climate change and economic policy. The methods for computing footprints
originate in the field of *input-output analysis*, which traces through networks
of economic dependency to link up consumption activities with the production
activities---and resulting emissions---which sustain them. This allows not only
calculating how much carbon is necessary to support someone's lifestyle, but
also determines the geographic spread of emissions, linking up the consumption practices
of one region with pollution in another.

{% maincolumn_html 'assets/html/co2con_net.html' 'This interactive figure shows
the network of "carbon dependencies" across the globe. Hover over a node to see
the region. An arrow pointing from, say, "South America" to "Europe" indicates
that emissions produced in South America are a part of the European carbon
footprint.' 90 550 %}

Input-output analysis rests on a number of assumptions. We analyzed the
consequences of these assumptions in [(Loomis, Cooper & Crutchfield
2021)](https://arxiv.com/abs/2106.03948). The upshot is that whether a nation's
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

<hr class="slender">
{% newthought " *Rome wasn't built in a day.* " %} *And that would be crazy, because
this website is far less complicated and also wasn't built in a day. I'll add
more project details soon.*