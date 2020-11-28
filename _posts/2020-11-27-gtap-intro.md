---
layout: post
title:  "Production, consumption and capital: Introduction"
date:   2020-11-27 16:00:00 -0800
categories: geography gtap 
excerpt: "I describe how GTAP data was processed and combined with external data sets to form a base dataset of global monetary flows and regional inputs of labor, energy and carbon emissions."
visible: 1
---
# Production, consumption and capital: Introduction

In this post, I describe how GTAP data was processed and combined with external data sets to form a base dataset of global monetary flows and regional inputs of labor, energy and $$\mathrm{CO}_2$$ emissions. This is a prelude to further posts where I explore how labor (measured in human-years, $$\mathrm{HY}$$), energy extraction/dissipation (measured in megatons of oil equivalent, $$\mathrm{MTOE}$$), and carbon emissions (measured in megatons of carbon dioxide, $$\mathrm{MTCO}_2$$) power worldwide consumption, and furthermore, how these activities are stimulated by capital investment. The dataset used is `GTAP 8` and is primarily geographical: it tracks production, consumption, investment and industrial activities on national and regional scales (Narayanan et. al., 2012). This means we can track the international flows of capital and embodied labor/energy/emissions, how such things flow within a nation are not available. Furthermore, the dataset we are using aggregates the extremely large and diverse world of industry into $$57$$ sectors, further limiting the scale of our analysis. Finally, `GTAP 8` only contains national-level information for $$114$$ countries; the rest of the world's nations are aggregated into $$20$$ regions. These aggregated regions only account for $$5.5 \%$$ of global trade.

Our goal, in essence, is to track two parallel and even somewhat dual phenomena. The first the support of worldwide consumption by irreversible processes, and regional inequalities in this support. Irreversible processes may involve the extraction of industrial energy from the environment, the dissipation of said energy, the expenditure of labor-time by workers, and the emission of pollutants, in particular $$\mathrm{CO}_2$$. (These four can be approximated with the data in this notebook; other irreversible processes involving more general forms of environmental degradation, the extraction/dissipation of energy by biological processes, and additional pollutants beyond carbon should also be studied.) "Regional inequalities" refers to the idea that localized irreversible processes do not necessarily occur to support consumption within their locality, but instead occur to support consumption in another region where irreversible processes may occur to a lesser degree. In other words, those who benefit from irreversible processes are not necessarily those who most directly experience their consequences.

The second phenomenon is the role of global capital and investment in generating regional inequalities. Dual to the "linear" model outlined above, in which irreversible processes are embodied by their products which travel from production to consumption, is the "circular" model of global monetary flow. There is a thermodynamic aspect to the global economy in this sense: just as biological and environmental cycles are inseparably tied to the irreversible progression of solar energy to final dissipation, so too is global capital circulation inseparable from its underlying irreversible processes. 

Therefore, not only can one track how an irreversible process in region $$A$$ ultimately supports consumption in region $$B$$, but furthermore we can identify how capital investment originating in region $$B$$ stimulate irreversible processes in region $$A$$. This latter "capital circulation" paradigm is distinct from the former "linear consumption" paradigm, but both capture the concept of regional inequalities in complementary ways. Each results in a matrix linking the local sectors where irreversible processes occur to final consumption or original investment. The investment matrix may be calculated directly from the `GTAP 8` data; tracking the flow of irreversible processes from origin to consumption requires making assumptions that allow us to utilize the same dataset. We will detail the computation and assumptions in this notebook.

Our work is inspired by similar work in the field of quantitative geography; particularly those by (Bergmann, 2012) and (Prell et. al., 2014). Those works focused on $$\mathrm{CO}_2$$ emissions, while here we expand this to also look at energy extraction/dissipation and labor. This notebook is intended as a preliminary investigation into these questions, with more sophisticated explorations to follow in order to build on previous work.

## The global social-accounting matrix

Most of the `GTAP 8` database is summed up by a series of regional *social-accounting matrices* (SAMs), which register direct interactions between various economic sectors. The value at row $$i$$ and column $$j$$ records the total amount of money paid by sector $$j$$ to sector $$i$$ over a given time period (in the case of `GTAP 8`, this time period is the years 2004 and 2007). The structure of a regional SAM, as it is stored in GTAP 8, is given by the table below:

<div class="table-wrapper" markdown="block" style="overflow:scroll">

|      | Domestic | Imports | Factors | Regional Household | Taxes | Investment | Consumption | Exports | Margins | Global capital | 
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Domestic** | `DIND` | | | | | `DINV` | `DCON` | `XIND` | `MARGIND` | |
| **Imports** | `MIND` | | | | | `MINV` | `MCON` | | | |
| **Factors** | `FIND` | | | | | | | | | |
| **Regional Household** | | | `RHHF` | | `RHHTAX` | | | | | |
| **Taxes** | `DTAX` | `MTAX` | `FTAX` | | | `INVTAX` | `CONTAX` | | | |
| **Investment** | | | `INVF` | `INVRHH` | | | | | `INVMARG` | `INVCAP` |
| **Consumption** | | | | `CONRHH` | | | | | | |
| **Exports** | | `XIND`$${}^{\top}$$ | | | | | | | | |
| **Margins** | | `MARG` | | | | | | | | |
| **Global Capital** | | | | | | | | | | |

</div>

The sectors of a regional SAM fall into 10 primary groups:

1. **Domestic industry**: These are the industrial sectors operating within a given region. For each region, there are $$57$$ commodity sectors describing domestic industry.
2. **Imports**: These are all imported goods, characterized again by the $$57$$ commodity sectors.
3. **Factors**: Factors of production are the regional endowments which supply the necessary resources for industrial activity. For each region, there are $$5$$ factors: Land (`Land`), Natural Resources (`NatRes`), Capital (`Capital`), skilled labor (`SkLab`) and unskilled labor (`UnSkLab`).
4. **Regional Household**: An aggregation of all private and public "households" within a region; all personal income and government revenue for a region is channeled through this sector.
5. **Taxes**: Taxes paid by sectors on top of other transactions.
6. **Investment**: One of the "Final Demand" sectors, this form of demand represents money spend by private investors buying equity in commodity sectors.
7. **Consumption**: The other two "Final Demand" sectors are categorized under consumption. These correspond to private (`PRIV`) and government (`GOVT`) consumption.
8. **Exports**: Tracks how **Domestic** sectors send goods to (and receive money from) the **Imports** sectors in other regions.
9. **Margins**: Unlike all other sectors, these final two (**Margins** and **Global Capital**) are not tied to regions. **Margins** is a global pool to which **Imports** sectors pay transportation costs, and from which **Domestic** transportation sectors receive payment. Imbalances in margins costs are reinvested.
10. **Global Capital**: Unlike all other sectors, these final two (**Margins** and **Global Capital**) are not tied to regions. **Global Capital** is a global pool through which direct foreign investments take place.

The central conceit of social-accounting matrices is that sectoral accounts must balance; that is, for each sector, the sum of that sector's row and column must be equal. The root of this assumption is that every institution must balance payments. This assumption somewhat fails with the `GTAP 8` SAM: the **Exports** sector does not represent a coherent institution, and only exists to stitch together regional SAMs. Only the **Exports**,  **Global capital** and **Margins** altogether are balanced, as these reflect the coherent collection of all institutions outside the given region. In the global SAM constructed by stitching together all regional SAMs, the **Exports** sector no longer exists and so all sectors can be balanced.

The sector groups **Global capital**, **Investment** and **Taxes** correspond to financial instruments which, while relevant for the financial analysis, are not required for studying the physical basis of consumption. We run the code involving the linear consumption paradigm and the financial circulation paradigm in a separate notebooks (`GTAP_LifecycleFlows-Computation.ipynb` and `GTAP_Leontief-Computation.ipynb`, respectively).

Below we load all the sub-matrices relevant to the physical basis of consumption. Note in our code that **Investment** (code: `INV`) and **Consumption** (code: `CON`) are initially contained together as the **Final Demand** (code: `DEM`) group.

## Correcting signed values

Certain submatrices–––specifically, those involving tax, investment and the "global sectors" (**Margins** and **Global capital**)–––are *signed*, which means they may be positive or negative in value. It is preferable for our purposes to treat a negative value from sector $$i$$ to $$j$$ as instead a *positive* value from $$j$$ to $$i$$. This will not alter the balance of the rows and columns, but will be more amenable to the stochastic methods we wish to use. Taxes (code: `TAX`) which are negative are recast as subsidies (code: `SUB`), which form a new sector.

<div class="table-wrapper" markdown="block" style="overflow:scroll">

|      | Domestic | Imports | Factors | Regional Household | Taxes | Subsidies | Investment | Consumption | Exports | Margins | Global capital | 
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Domestic** | `DIND` | | | | | `DSUB` | `DINV` | `DCON` | `XIND` | `MARGIND` | |
| **Imports** | `MIND` | | | | | `MSUB` | `MINV` | `MCON` | | | |
| **Factors** | `FIND` | | | | | `FSUB` | | | | | |
| **Regional Household** | | | `RHHF` | | `RHHTAX` | | `RHHINV` | | | | |
| **Taxes** | `DTAX` | `MTAX` | `FTAX` | | | | `INVTAX` | `CONTAX` | | | |
| **Subsidies** | | | | `SUBRHH` | | | | | | | |
| **Investment** | | | `INVF` | `INVRHH` | | `INVSUB` | | | | `INVMARG` | `INVCAP` |
| **Consumption** | | | | `CONRHH` | `CONSUB` | | | | | | |
| **Exports** | | `XIND`$${}^{\top}$$ | | | | | | | | | |
| **Margins** | | `MARG` | | | | | `MARGINV` | | | | |
| **Global Capital** | | | | | | | `CAPINV` | | | | |

</div>

This only requires changes to submatrices which involve financial instruments (**Global capital**, **Investment**, and **Taxes**) and so is handled in the notebook `GTAP_Leontief-Computation.ipynb`.

## Irreversible processes: energy, emissions and labor

In addition to regional and global SAMs,  the `GTAP 8` dataset also provides information on the *energy volumes* involved in transactions with energy sectors, as well as the $$\mathrm{CO}_2$$ emissions which result from industrial activities and consumption. The emissions data by itself directly attests to and quantifies an irreversible process of interest and does not require much additional work to interpret. However, we must consider how to best approach the energy dataset.

The structure of the energy data is given by the following table. Note that here, energy flows in the *opposite* direction to money: an entry in row $$i$$ and column $$j$$ indicates a transaction in which energy flowed from sector $$i$$ to sector $$j$$.

<div class="table-wrapper" markdown="block" style="overflow:scroll">

|      | Domestic | Imports | Factors | Regional Household | Taxes | Investment | Consumption | Exports | Margins | Global capital | 
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Domestic energy** | `DERG` | | | | | `DERGINV`* | `DERGCON` | `XERG` | | |
| **Imported energy** | `MERG` | | | | | `MERGINV`* | `MERGCON` | | | |
| **Exports** | | `XERG`$${}^{\top}$$ | | | | | | | | |

</div>

\* *The asterisks on `DERGINV` and `MERGINV` indicate that these are extremely small in magnitude (their total contribution is 5 orders of magnitude less than the the total contribution from `DERGCON` and `MERGCON`) and as I am not even certain how energy purchases by investment are meant to be interpreted, I have chosen for now to assume these are data entry errors pending further understanding. As such these will be excluded from further consideration.*

The submatrices `DERG`, `MERG` and `XERG` correspond to the energetic commoditity sectors `ERG`, with `D`, `M` and `X` referring to domestic, imported and exported commodities as before. The `ERG` commodity sectors are as follows:

1. `coa`: Coal extractors and intermediaries
2. `oil`: Oil extractors and intermediaries
3. `gas`: Natural gas extractors and intermediaries
4. `p_c`: Manufacture of coke oven and refined petroleum products, as well as nuclear fuel
5. `ely`: Production, collection and distribution of electricity (including from renewable sources)
6. `gdt`: Manufacture and distribution of gas, steam and hot water

Any of these sectors may be involved in original extraction of energy from the environment, and any may function as a simple intermediary which does not extract new energy and may, in fact, be a net dissipator during the refining or distribution process. The current aggregation of data does not offer a clear way to separate the processes of extraction and dissipation for these industries. To make do, we consider the difference between summing over rows and columns corresponding to these sectors–––that is, the difference between output and input. A positive value indicates that a net amount of energy was extracted by the industry; a negative value indicates that net energy was dissipated. 

For each region-commodity pair $$(r,i)$$, we define the dissipation and extraction as

<div class="eqn-wrapper" markdown="block" style="overflow:scroll">

$$
\mathtt{EXTR}_{r,i} = \max\left(0,\sum_{j}\mathtt{DERG}_{r,i,r,j} + \sum_{s\neq r\\ j}\mathtt{XERG}_{r,i,r,j} + \sum_{c} \mathtt{DERGCON}_{r,i,r,c} - \sum_{j}\mathtt{DERG}_{r,j,r,i} - \sum_{j}\mathtt{MERG}_{r,j,r,i}\right)
$$

</div>

<div class="eqn-wrapper" markdown="block" style="overflow:scroll">

$$
\mathtt{DISS}_{r,i} = -\min\left(0,\sum_{j}\mathtt{DERG}_{r,i,r,j} + \sum_{s\neq r\\ j}\mathtt{XERG}_{r,i,r,j} + \sum_{c} \mathtt{DERGCON}_{r,i,r,c} - \sum_{j}\mathtt{DERG}_{r,j,r,i} - \sum_{j}\mathtt{MERG}_{r,j,r,i}\right)
$$

</div>

The total sums (over *all* commodity sectors) must balance: 

$$
\sum_{r,i} \mathtt{EXTR}_{r,i} = \sum_{r,i} \mathtt{DISS}_{r,i}
$$

If $$i$$ is not in `ERG` (that is, it is in some non-energetic industry) then $$\mathtt{EXTR}_{r,i}$$ will always be zero–––non-energetic industries are always dissipative. This exclusive measurement of net-extraction or net-dissipation for each sector over the time period of the dataset will function as a stand-in proxy for a more accurate assessment of total dissipation and extraction by each industry, as parallel processes.

We can also compute the dissipation due to direct consumption (such as from burning gasoline for cars, or running the air conditioner in the summer) as $$\mathtt{DISSCON}_{r,i} = \mathtt{DERGCON}_{r,i}+\mathtt{MERGCON}_{r,i}$$.

The net energy extracted from each region and the net energy dissipated by the same
are displayed below.

<iframe
  src="/assets/gtap_graphs/extr_map.html"
  style="width:100%; height:650px;"
></iframe>

<iframe
  src="/assets/gtap_graphs/diss_map.html"
  style="width:100%; height:650px;"
></iframe>

The structure of the carbon emissions dataset is considerably simpler:

<div class="table-wrapper" markdown="block" style="overflow:scroll">

|      | Domestic | Imports | Factors | Regional Household | Taxes | Investment | Consumption | Exports | Margins | Global capital | 
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Domestic emissions** | `DCO2` | | | | | | `DCO2CON` | | | |
| **Imported emissions** | `MCO2` | | | | | | `MCO2CON` | | | |

</div>

The commodity sector group `CO2` contains 5 sectors: in fact, it contains all of the `ERG` sectors except `ely`. An entry in row $$i$$ and column $$j$$ indicates that sector $$j$$ purchased and utilized some form of energy from sector $$i$$, resulting in a certain amount of $$\mathrm{CO}_2$$ emissions. From these we compute

$$
\mathtt{CO2}_{r,i} = \sum_{j} \mathtt{DCO2}_{r,j,r,i} + \sum_{j} \mathtt{MCO2}_{r,j,r,i}
$$

$$
\mathtt{CO2CON}_{r,i} = \sum_{j} \mathtt{DCO2CON}_{r,j,r,i} + \sum_{j} \mathtt{MCO2CON}_{r,j,r,i}
$$

As best as I can tell, GTAP 8 only reports total $\mathrm{CO}_2$ emissions over the year 2007. The resulting
regional emissions for this year are reported on the map below.

<iframe
  src="/assets/gtap_graphs/co2_map.html"
  style="width:100%; height:650px;"
></iframe>

Lastly, we consider the role of *human labor* in the global economy. The `GTAP 8` dataset does not provide sufficient information to determine the actual amount of labor, quantified in human-years, was involved in productive processes; however, it does provide the total amount of wages/salary paid out to labor by each sector (through the `SkLab` and `UnSkLab` factors). I combined this with estimates from the International
Labor Organization statistical database (ILOSTAT), which provided the labor force and the estimated percentage
of unutilized labor due to unemployment and time-based underemployment (this metric is called LU2).

By combining these two datasets, we can approximate the proportion of the labor force involved in each sector based on total wages paid. This approximation will tend to overestimate total labor for industries employing higher-paid skilled laborers and underestimate the same for industries which employ more unskilled laborers. Absent more complete data, it will have to do. Furthermore, incomplete data for very small countries and underdeveloped countries means that the labor force in such regions will be further underestimated. This issue does not impact nations which have their own region in the `GTAP 8` database and so only impacts a small percentage of international trade. 

In any case, this results in a total labor cost over the time period for each region $$r$$ and commodity sector $$i$$:

$$
\mathtt{LAB}_{r,i} = \mathtt{EMPLOYED}_{r}\cdot \frac{\mathtt{FIND}_{r,\mathtt{SkLab},r,i}+\mathtt{FIND}_{r,\mathtt{UnSkLab},r,i}}{\sum_{j}\left(\mathtt{FIND}_{r,\mathtt{SkLab},r,j}+\mathtt{FIND}_{r,\mathtt{UnSkLab},r,j}\right)}
$$

The estimated average wage which results from our employment estimates is not the same
as the average salary of full-time employees or income-per-capita. It is the total amount
of money paid over the time period divided by the estimated total human-years of labor
contributed by both full-time and part-time workers. As such, it tends to run much lower than the other
two mentioned metrics, skewing closer to the minimum wage in countries
where a significant portion of labor is part-time. We display this average wage below.

<iframe
  src="/assets/gtap_graphs/wage_map.html"
  style="width:100%; height:650px;"
></iframe>

Finally, we map out the total estimated labor-time contributed by each nation
during 2004 and 2007
based on our calculations.

<iframe
  src="/assets/gtap_graphs/lab_map.html"
  style="width:100%; height:650px;"
></iframe>

These results are not far off what we would expect of a population map,
which is quite reasonable–––fluctuations from this ideal
would result from labor underutilization and differences in age distribution.