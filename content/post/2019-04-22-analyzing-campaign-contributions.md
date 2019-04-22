---
title: Analyzing Campaign Contributions
author: Sono Shah
date: '2019-04-22'
slug: analyzing-campaign-contributions
categories: []
tags:
  - Asian Americans
  - FEC
image:
  caption: ''
  focal_point: ''
---

Last week, I took a closer look at the APRIL FEC Quarterly reports from the 14 major democratic candidates competing for the presidential nomination in 2020. Specifically, I looked at who Asian donors were *giving to* and which candidates were *raising the most from* Asian contributions. Check out the first post on Asian contributions overall [here](http://aapidata.com/blog/who-is-winning-asian-donors2020q1/) and the second one which looks at specific ethnic groups [here](http://aapidata.com/blog/who-is-winning-asian-donors2020q1-partb/). I hope this post helps explain how I analyzed the contribution data, and what kind of caveats should be considered. If you have any questions please send me an email or message me on Twitter!


![Asian American Contributions (April 2019 FEC)](/img/asian_contribs/asian-donors-to-dem-2019Q1.png)

![Asian American Contributions by Ethnic Group (April 2019 FEC)](/img/asian_contribs/part2-ethnic-totals.png)


## Basic Steps of analysis

Here's the basic steps of the analysis from data collection to final estimates. Most of the cleaning/analysis was done in `R`, which I strongly recommend to everyone  :) [#Tidyverse4life](https://www.tidyverse.org/).

1. Scrape April 2019 quarterly filings for each candidate into a database^[You can manually download them, but I would strongly recommend using Fec-Loader]
2. Subset to only those classified as individual contributions ^[Using `entity_type` field in contribution record]
3. Geocode contributor information^[Ideally, you want the smallest possible geography possible (i.e. census block), for this analysis, I geocoded each contribution record to the census tract. The `R` package I used also allows for county and place as well.]
4. Estimate race/ethnicity of contributor
5. Subset to Asian contributions and estimate ethnicity for top 6 Asian ethnic groups in the US^[I used an Asian detailed origin surname list from [Lauderdale & Kestenbaum](https://link.springer.com/article/10.1023/A:1026582308352)]


## What are the caveats with this data?

### Itemized individual contributions

Due to FEC requirements on reporting, the only data that is publicly available for analysis are those that are classified as "itemized individual contributions". These contributions are those that are either required to be reported to the FEC due to the amount (>$200). 

### Doesn't this mean that your analysis excludes small donors?

> Yes, but **not entirely**.

In recent years, many Democratic campaigns have turned to using [ACTBLUE](https://secure.actblue.com/) to help with fundraising efforts, particularly among small donors ([NYT](https://www.nytimes.com/2014/10/09/upshot/how-actblue-became-a-powerful-force-in-fund-raising.html), [Wired](https://www.wired.com/2015/11/actblues-one-click-donations-are-changing-the-2016-presidential-race/)). Since ACTBLUE is defined as political action committee (PAC), they are subject to slightly different reporting requirements which allows us a peek into small donors. When a donor gives to a particular through ACTBLUE's platform, that contribution is still counted as an individual contribution, but ACTBLUE acts as an intermediary who then delivers the contributions to the candidate's campaign committee. In fact in 2018, FiveThirtyEight published [an excellent piece](https://fivethirtyeight.com/features/how-actblue-is-trying-to-turn-small-donations-into-a-blue-wave/) about ACTBLUE that leveraged this data to look at small donor contribution patterns.  

Taking Andrew Yang's [filing](https://www.fec.gov/data/committee/C00659938/) as an example, we can see that his principle campaign committee "Friends of Andrew Yang" reported raising over **1.7 million** dollars in individual contributions during this time period, ~342K of which are considered **itemized individual contributions**. Looking closer at the [itemized contributions](https://www.fec.gov/data/receipts/?two_year_transaction_period=2020&cycle=2020&data_type=processed&committee_id=C00659938&min_date=01%2F01%2F2019&max_date=12%2F31%2F2020&line_number=F3P-17A) we can see that many of them are given through ACTBLUE and some of the contributions are well under $200. So, looking back at my posts, Andrew Yang's $119,440 that he raised from Asian American contributions is estimated from the *itemized individual contributions* **only** since we don't have any data on the contributors who are grouped into **unitemized individual contributions**.

> **Caveat #1**: We can't look at *unitemized contributions*, but that doesn't mean we can't look at contributions made by smaller donors.

## Ethnic surname analysis

Ethnic surname analysis is a technique for imputing the race/ethnicity of a person using their last name (surname) and Census data on surnames by racial/ethnic group. Relatively recently, scholars have improved on this method by incorporating more information about the person you are trying to impute race/ethnicity for by using geocoded demographic information. This particular flavor of ethnic surname analysis has been called many different things, but the version that I'm most familiar with has been called "Bayesian Improved Surname Geocoding" or BISG. 

The caveats associated with this approach is beyond the scope of this post but I have listed several links at the bottom that are helpful in outlining the general approach. One caveat that I will mention here is the opportunity for contributors to be miscoded due to interracial marriage. According to [estimates from PEW](https://www.pewresearch.org/fact-tank/2017/06/12/key-facts-about-race-and-marriage-50-years-after-loving-v-virginia/), nearly 3 in 10 Asian newlyweds were married to someone of a different race/ethnicity in 2015, the highest of any racial group. Unfortunately this is something that we don't have a good solution for, so it is important to keep this in mind when using these methods.

However, it is worth noting that this type of analysis has been used in Health research ([Elliot et al 2008](https://dx.doi.org/10.1111%2Fj.1475-6773.2008.00854.x), [Adjaye-Gbewonyo et al 2013](https://doi.org/10.1111/1475-6773.12089); [Grundmeier et al 2015](https://doi.org/10.1111/1475-6773.12295)), political science ([Imai & Khanna](https://doi.org/10.1093/pan/mpw001); [Fraga 2015](https://onlinelibrary.wiley.com/doi/abs/10.1111/ajps.12172)), and even by the [Consumer Finance Protection Bureau](https://www.consumerfinance.gov/data-research/research-reports/using-publicly-available-information-to-proxy-for-unidentified-race-and-ethnicity/) to help enforce fair lending laws. In addition, Catalist a data vendor that often supplies Democratic campaigns (and academic researchers) with enriched voter file data bases their approach to modeling race/ethnicity from this method as well ([Hersch](https://books.google.com/books?hl=en&lr=&id=DEuqCQAAQBAJ&oi=fnd&pg=PR7&dq=hacking+the+electrorate&ots=NSFxnh_DvD&sig=Syibag0Mh3z3xGjSCbs6pJAxibM); [Fraga 2018](https://doi.org/10.1017/9781108566483))^[See Appendix A3 for a discussion on Estimating Race/Ethnicity with Catalist Data].


> **Caveat #2**: Ethnic-surname analysis to group donors is a widely-used technique for imputing race/ethnicity on administrative records, **but** there are important caveats (i.e. rates of interracial marriage) to be aware of. 


### Tools for Analysis

- [FEC-Loader](https://github.com/PublicI/fec-loader): I strongly recommend using this tool to parse/store raw FEC data. [Postico](https://eggerapps.at/postico/) is great for a simple user interface. R has great packages for connecting to databases as well.

- Geocoding Tool (there are many, here are some links [Census Geocoder](https://geocoding.geo.census.gov/), [Data Science Toolkit](http://www.datasciencetoolkit.org/),[Texas A&M Geocoder](http://geoservices.tamu.edu/Services/Geocode/))

- Ethnic Surname Analysis: [WRU](https://github.com/kosukeimai/wru) (Imai & Khanna 2018)


### List of scholarship on ethnic surname analysis

- Adjaye‐Gbewonyo, D., Bednarczyk, R. A., Davis, R. L., & Omer, S. B. (2014). Using the Bayesian Improved Surname Geocoding Method (BISG) to create a working classification of race and ethnicity in a diverse managed care population: a validation study. Health Services Research, 49(1), 268-283.

- Imai, K., & Khanna, K. (2016). Improving ecological inference by predicting individual ethnicity from voter registration records. Political Analysis, 24(2), 263-272.

- Elliott, M. N., Fremont, A., Morrison, P. A., Pantoja, P., & Lurie, N. (2008). A new method for estimating race/ethnicity and associated disparities where administrative records lack self‐reported race/ethnicity. Health services research, 43(5p1), 1722-1736.

- Fiscella, K., & Fremont, A. M. (2006). Use of geocoding and surname analysis to estimate race and ethnicity. Health services research, 41(4p1), 1482-1500.

- Fraga, B. L. (2016). Candidates or districts? Reevaluating the role of race in voter turnout. American Journal of Political Science, 60(1), 97-122.

- Fraga, B. L. (2018). The Turnout Gap: Race, Ethnicity, and Political Inequality in a Diversifying America. Cambridge University Press.

- Grundmeier, R. W., Song, L., Ramos, M. J., Fiks, A. G., Elliott, M. N., Fremont, A., ... & Localio, R. (2015). Imputing missing race/ethnicity in pediatric electronic health records: reducing bias with use of US census location and surname data. Health services research, 50(4), 946-960.

- Hersh, E. D. (2015). Hacking the electorate: How campaigns perceive voters. Cambridge University Press.

- Lauderdale, D. S., & Kestenbaum, B. (2000). Asian American ethnic identification by surname. Population Research and Policy Review, 19(3), 283-300.


