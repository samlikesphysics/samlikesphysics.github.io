---
layout: post
title:  "Production, consumption and capital: Net flows"
date:   2020-11-27 18:00:00 -0800
categories: geography gtap 
excerpt: "I use network visualizations to perceive directional relationships between regions of the globe."
visible: 1
---

<div class="button-wrapper" markdown="block" style="overflow:scroll;font-size:120%" align="center">

$$\left<\right.$$ [**Importers and exporters**](/geography/gtap/2020/11/27/gtap-mx.html) $$\|$$ [**Home**](/geography/gtap/)

</div>

# Production, consumption and capital: Net flows

In this post, I use network visualizations to perceive directional relationships between regions of the globe. This is mostly for fun but in part for better understanding. Previously we looked at net exporters and importers of resources; here, we will get a sense of where those exports are going, or from whence the imports come. There is a tradeoff–––to usefully visualize this, it is necessary to group countries together in order to reduce visual noise. The following categorizations are modified slightly from those used in (Bergmann, 2012).

The above charts show whether nations are net exporters or importers of extracted energy; however, they do not show to whom exports occur by region, or from whence imports have come. The next two visualizations have clustered countries into *megaregions* determined by the GTAP database. The megaregions are as follows:

<div class="table-wrapper" markdown="block" style="overflow:scroll">

| MEGAREGION | Regions |
| :---: | :--- |
| **CHINA** | China* |
| **OCEANIA** | Australia, New Zealand, XOC (Papua New Guinea, Marshall Islands, American Samoa, Cook Islands, Fiji, Micronesia, Guam, Kiribati, Northern Mariana Islands, New Caledonia, Norfolk Island, Niue, Nauru, Palau, French Polynesia, Solomon Islands, Tokelau, Tonga, Tuvalu, Vanuatu, Wallis and Futuna Islands, Samoa) |
| **EAST ASIA** | Japan, South Korea, Taiwan, Hong Kong, Singapore**, XEA (Macau, North Korea) |
| **SOUTHEAST ASIA** | Indonesia, Cambodia, Laos, Myanmar, Thailand, Vietnam, Malaysia, Philippines, XSE (Brunei, East Timor) |
| **SOUTH ASIA** | India, Nepal, Bangladesh, Pakistan, Sri Lanka |
| **NORTH AMERICA** | United States, Canada, XNA (Bermuda, Greenland, Saint Pierre, Miquelon) |
| **SOUTH AMERICA** | Brazil, Argentina, Bolivia, Chile, Colombia, Ecuador, Paraguay, Peru, Uruguay, Venezuela, XSM (French Guiana, Falkland Islands, Guyana, Suriname, Belize) |
| **C. AMERICA & CARIBBEAN** | Mexico, Costa Rica, Guatemala, Nicaragua, Panama, Honduras, XCA (Belize, El Salvador), XCB (Dominican Republic, Aruba, Anguilla, former Netherlands Antilles, Antigua and Barbuda, Bahamas, Barbados, Cuba, Cayman Islands, Dominica, Guadeloupe, Grenada, Haiti, Jamaica, Saint Kitts and Nevis, Saint Lucia, Montserrat, Martinique, Puerto Rico, Turks and Caicos Islands, Trinidad and Tobago, Saint Vincent and the Grenadines, British Virgin Islands, United States Virgin Islands) |
| **WESTERN EUROPE** | Austria, Belgium, Denmark, Finland, France, Germany, Ireland, Italy, Luxembourg, Malta, Netherlands, Portugal, Spain, Sweden, Great Britain, Switzerland, Norway, XEF (Iceland, Liechtenstein) |
| **EASTERN EUROPE** | Cyprus, Czech Republic, Estonia, Greece, Hungary, Latvia, Lithuania, Poland, Slovakia, Slovenia, Albania, Bulgaria, Croatia, Romania, Bosnia and Herzegovina, XER (Andorra, Faroe Islands, Gibraltar, Monaco, Macedonia, San Marino, Serbia, Vatican City)|
| **FORMER USSR** | Belarus, Russia, Ukraine, Kazakhstan, Kyrghyzstan, Armenia, Azerbaijan, Georgia, Mongolia***, XEE (Moldova), XSU (Tajikistan, Turkmenistan, Uzbekistan) |
| **WEST ASIA** | Bahrain, Iran, Israel, Kuwait, Oman, Qatar, Saudi Arabia, Turkey, United Arab Emirates, XWS (Iraq, Jordan, Lebanon, Palestine, Syria, Yemen) |
| **NORTH AFRICA** | Egypt, Morocco, Tunisia, XNF (Algeria, Libya, Western Sahara) |
| **WEST AFRICA** | Benin, Burkina Faso, Ivory Coast, Ghana, Guinea, Nigeria, Senegal, Togo, XWF (Mali, Cape Verde, Gambia, Guinea-Bissau, Liberia, Mauritania, Niger, Saint Helena, Sierra Leone) |
| **MIDDLE AFRICA** | Cameroon, XAC (Angola, Democratic Republic of the Congo), XCF (Central African Republic, Republic of the Congo, Gabon, Equatorial Guinea, Sao Tome and Principe, Chad) |
| **EAST AFRICA** | Ethiopia, Kenya, Madagascar, Malawi, Mauritius, Mozambique, Rwanda, Tanzania, Uganda, Zambia, Zimbabwe, XEC (Burundi, Comoros, Djibouti, Eritrea, Mayotte, Reunion, Sudan, Somalia, Seychelles) |
| **SOUTHERN AFRICA** | South Africa, Botswana, Namibia, XSC (Lesotho, Swaziland) |
| **XTW** | Antarcica, French Southern Territories, Bouvet Island, British Indian Ocean Territory |

*\* China is placed in a category on its own due to its size and its distinct economic nature from the other East Asian countries.*

*\*\* Singapore was included in East Asia as a part of "Greater China," i.e. those nations strongly influenced by Han culture, and because of its close ties and economic similarities with other East Asian countries.*

*\*\*\* Mongolia was included in the "Former USSR" category despite its independence as its historical trajectory closely mirrors other Central Asian countries which were in the USSR, and it shares structural similarities in its extractive industries.*

</div>

## Energy extraction

The following network indicates by directed edges the *net flow* of extracted energy to consumption between the two regions. That is, for two megaregions $$R$$ and $$S$$, the edge weight is given by

$$
E_{R\rightarrow S} = \max\left(0,\sum_{r\in R, s\in S\\i,j} \mathtt{EXTRCONL}_{r,i\rightarrow s,j} - \sum_{r\in R, s\in S\\i,j} \mathtt{EXTRCONL}_{s,i\rightarrow r,j}\right)
$$

To put it another way, an arrow points from megaregion $$R$$ to megaregion $$S$$ if there is a net flow of extracted energy from $$R$$ to $$S$$, and the opacity of the arrow indicates the magnitude of that net flow. 

In the visualization, the vertical position of a megaregion indicates its relative rank in terms of being a net exporter or importer, using the megaregion's P/C ratio.

<iframe
  src="/assets/gtap_graphs/extrcon_net.html"
  style="width:100%; height:700px;"
></iframe>

The next network is similar; it indicates by directed edges the net flow of extracted energy to *investment* between the two megaregions. The edge weight is given by

$$
E_{R\rightarrow S} = \max\left(0,\sum_{r\in R, s\in S\\i,j} \mathtt{EXTRINVL}_{r,i\rightarrow s,j} - \sum_{r\in R, s\in S\\i,j} \mathtt{EXTRINVL}_{s,i\rightarrow r,j}\right)
$$

Megaregions are now vertically positioned in order of their P/I ratio.

<iframe
  src="/assets/gtap_graphs/extrinv_net.html"
  style="width:100%; height:700px;"
></iframe>

There is not a large amount of difference between the two networks; both appear to be mostly directed acyclic graphs, with clear "sources" and "sinks" of energy and many intermediate nodes. Overall, extracted energy primarily originates from megaregions in the upper-right of the graph, mostly from `WEST ASIA`. The primary importer of extracted energy is the `EAST ASIA` followed by `WESTERN/EASTERN EUROPE`; intermediate regions in the network flow include the `AMERICA`s, `CHINA` and `SOUTHEAST ASIA`.

## Energy dissipation

We can also study the net imports and exports of embodied *dissipation* by visualizing it as a directed acyclic network over megaregions. Below, we see that in the consumption paradigm, `SOUTHERN AFRICA`, `CHINA` and `SOUTHEAST ASIA` are the predominant exporters, with significant intermediate regions including `SOUTH ASIA`, `SOUTH AMERICA`, `EASTERN EUROPE` and `EAST/WEST ASIA`. Primary importers of embodied dissipation include both highly prosperous regions such as `NORTHERN AMERICA` and `WESTERN EUROPE`, as well as impoverished regions such as `WEST/EAST/MIDDLE AFRICA`. It is worth noting the arrow from `NORTHERN AMERICA` to `EFTA`.

<iframe
  src="/assets/gtap_graphs/disscon_net.html"
  style="width:100%; height:700px;"
></iframe>

There are noteworthy changes in the investment network. First, we note how both `CHINA` and `EAST ASIA` shift significantly downwards in their relative positions; as sources of investors, these regions soften the degree to which they are net exporters by owning stake in their own enterprises. However, `WESTERN EUROPE` remains the primary importer, even in its relationship with `NORTHERN AMERICA`, where the net flow of embodied dissipation only intensifies when we look at investment.

<iframe
  src="/assets/gtap_graphs/dissinv_net.html"
  style="width:100%; height:700px;"
></iframe>

## $$\mathrm{CO}_2$$ emissions

The similarity between dissipation and $\mathrm{CO}_2$ emissions continues when we consider the networks of net consumption and investment flows of embodied $\mathrm{CO}_2$ emissions; however, we note that `EAST ASIA` shifts significantly downwards towards the importers. That `EAST ASIA` is much more an exporter of dissipation than it is of carbon emissions is likely a signifier of the types of energy used. In comparison, essentially every other region moves *upwards* in their relative vertical position when we switch from looking at dissipation to emissions.

<iframe
  src="/assets/gtap_graphs/co2con_net.html"
  style="width:100%; height:700px;"
></iframe>

<iframe
  src="/assets/gtap_graphs/co2inv_net.html"
  style="width:100%; height:700px;"
></iframe>

## Labor time

Lastly, we look at the net flows of embodied labor between megaregions. Here we see the primary origin points of embodied labor as located in `CHINA`, `AFRICA` and `SOUTH/SOUTHEAST ASIA` with intermediate regions in `FORMER USSR`, `SOUTH/CENTRAL AMERICA`, and `EASTERN EUROPE`. The primary consuming megaregions are `OCEANIA`, `NORTH AMERICA` and `EUROPE`, followed by the still somewhat-intermediate `EAST ASIA` and `WEST ASIA`.

<iframe
  src="/assets/gtap_graphs/labcon_net.html"
  style="width:100%; height:700px;"
></iframe>

The net investment flow of labor looks quite similar. The primary distinction here is that `CHINA` and `EAST ASIA` move more decisively towards the intermediate zone. Just as with energy dissipation/carbon emissions, these regions are supporters of consumption but themselves provides some of its own regional investment. A similar phenomenon can be observed here for `EASTERN EUROPE`.

<iframe
  src="/assets/gtap_graphs/labinv_net.html"
  style="width:100%; height:700px;"
></iframe>

<div class="button-wrapper" markdown="block" style="overflow:scroll;font-size:120%" align="center">

$$\left<\right.$$ [**Importers and exporters**](/geography/gtap/2020/11/27/gtap-mx.html) $$\|$$ [**Home**](/geography/gtap/)

</div>