---
title: Democrats hold a big fundraising advantage over Republicans, but are actually
  losing market share among Asian donors
author: Sono Shah
date: '2019-04-01'
draft: TRUE
slug: 2018-midterms-young-kim
categories: []
tags:
  - Asian Americans
image:
  caption: ''
  focal_point: ''
---





> **UPDATE:** This is a post I had originally worked on for just before the 2018 midterms, but did not end up publishing it. Some of the references will be dated, but I think a lot of the differences in Asian contribution patterns are still worth thinking about



Earlier this month, Democratic hopes to retake the House were buoyed by reports of their massive fundraising advantage over Republican candidates as the Federal Election Commission (FEC) released fundraising figures from the third quarter of 2018 ([Link1](https://www.cnn.com/2018/10/16/politics/democrat-money-advantage-third-quarter-fundraising/index.html),  [Link2](https://ktla.com/2018/10/16/democrats-out-fundraising-california-republicans-by-millions-in-most-competitive-house-races/), [Link 3](https://www.washingtonpost.com/politics/paloma/the-trailer/2018/10/02/the-trailer-democrats-are-breaking-fundraising-records-republicans-blame-outsiders/5bb37b851b326b7c8a8d17be/), [Link 4](http://www.latimes.com/politics/la-pol-ca-california-republicans-fec-spending-20181016-story.html)) 

On the surface, the FEC data paints an optimistic picture for the Democratic Party and their chances for re-taking the House on election day. At the same time, the data also reveals some areas of concern for Democratic fundraising, specifically, among Asian donors.

My research shows that, while overall a larger share of all individual contributions are going to Democratic House candidates than in previous cycles, the Democratic share of Asian contributions has actually decreased in 2018 compared to previous cycles.

## Here’s how I did my research

I analyzed political contribution records of individual campaign contributions to House candidates using the 2014, 2016, and 2018 contribution files available from the FEC. Since the 2018 cycle is not complete, I subset contributions from 2014 and 2016 to include only those reported from Q1 to Q3 to match what is currently available from the FEC for this year.^[I subset contributions to House committees directly affiliated with a House candidate by using the Committee. Type codes and candidate ID numbers provided by the FEC.]  I estimated the race of each donor by using a popular ethnic surname analysis technique that has been used extensively by scholars in political science, and even by the Consumer Finance Protection Bureau to help enforcement of fair-lending laws.^[For my research, I used the R package WRU published by Kosuke Imai, and Kabir Khanna, the link to their github Repository is https://github.com/kosukeimai/wru]  

While House Democrats are raising a larger share of contributions overall, their share of Asian American contributions has decreased since 2014.




Focusing on midterm election years, among all individual contributions, the Republican share of money given to House candidates in 2014 was about 58%. In 2018, this number decreased to 54% percent, a slight decrease.^[Estimates of partisan share of individualized donors will differ from others due to the fact that I subset contributions records to include those that are complete enough to allow for ethnic surname analysis. Contribution records that are missing information like State and Zip code are necessarily excluded here.] 

Looking at the same time periods but among contributions from Asian donors, the Republican share was about 24% in 2014, but increased to 34% in 2018, more than double the change among all individual contributions and in the opposite direction.


<table class="table table-striped table-hover table-responsive" style="margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> GOP Share House Contributions </th>
   <th style="text-align:left;"> 2014 </th>
   <th style="text-align:left;"> 2018 </th>
   <th style="text-align:left;"> Change </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Asian Contributions </td>
   <td style="text-align:left;"> 24% </td>
   <td style="text-align:left;"> 34% </td>
   <td style="text-align:left;"> <span style="     color: green;">10%</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> All Individual Contributions </td>
   <td style="text-align:left;"> 58% </td>
   <td style="text-align:left;"> 54% </td>
   <td style="text-align:left;"> <span style="     color: red;">-4%</span> </td>
  </tr>
</tbody>
</table>

{{< figure library="1" src="asian_versus_total.png" title="A caption" >}}


The sharp increase remains even when including data from 2016 in the figure above. Asian contributions shift slightly more Republican from 2014 to 2016, but abruptly moved much more Republican in 2018.

**Why are we seeing such a large shift in the flow of money from Asian donors?**

The shift seems puzzling given that studies of Asian American political behavior suggest a growing partisan attachment to the Democratic Party in recent years. Data from the 2018 Asian American Voter Survey suggests that the majority of Asian American voters favor Democratic House candidates by a wide margin over Republicans (50% to 28%) and give the Democratic Party a large net favorability rating (58% to 28%) compared to the net unfavorable rating for the Republican Party (52% unfavorable).^[http://aapidata.com/wp-content/uploads/2018/10/2018-AA-Voter-Survey-report-Oct9.pdf] So, what could explain such a large shift in Asian contributions this cycle?

**Young Kim (CA-39)**

A closer look at the data reveals that while Asian donors are giving a greater share of their money to Republican candidates than in previous cycles, the money is heavily concentrated to one candidate, former California State Assemblywoman and Korean American, Young Kim. As of the Q3 filing, contributions to Kim’s committee have accounted for nearly 19% of all money Asian donors gave to Republican candidates which is a larger share than any single candidate received in 2016 or 2014, and nearly **double** that of the Republican candidate with the next largest share in 2018.

To get a better understanding of the extent to which Young Kim is responsible for the shift in contributions for 2018, I remove all contributions to Young Kim. As shown in Table 2, excluding contributions to Kim, we still see an increase in the Republican share of Asian contributions, but the shift is roughly **half** of the increase when looking at all Asian contributions.

<table class="table table-striped table-hover table-responsive" style="margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:left;"> GOP Share Asian Contributions </th>
   <th style="text-align:left;"> Change from 2014 </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> All Asian Contributions </td>
   <td style="text-align:left;"> 34% </td>
   <td style="text-align:left;"> <span style="     color: green;">10%</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> All Asian Contributions (w/out Kim) </td>
   <td style="text-align:left;"> 28% </td>
   <td style="text-align:left;"> <span style="     color: green;">4%</span> </td>
  </tr>
</tbody>
</table>

**Why Young Kim?**

Part of why Asian donors are giving so much money to Kim is likely because they want to support Asian American candidates.

Theories of representation suggest that citizens prefer representatives who are of the same racial or ethnic background as themselves. Empirical evidence for these claims however, are mixed.^[Prior work has uses the term coethnic to indicate preferences for same race and/or ethnicity. I use co-racial here.]  While some studies find that co-racial preferences exist among minority groups (Barreto 2007; Schildkraut, 2012), others find that co-racial preferences are primarily explained by partisan, ideological or policy preferences (Ansolabhere & Fraga 2016) or may be conditional (Michelson 2005, Wallace 2014). However, scholarship has almost exclusively focused on this question in the context of voting.

The extent to which Asian Americans are more likely to donate to co-racial candidates is a tougher test.

Understanding the extent to which Asian donors are willing to support Young Kim because of her racial or ethnic background is important for unpacking the relationship between racial/ethnic identity and political participation. 

Donating offers several important differences compared to voting that offer leverage for understanding preferences for descriptive representatives. First, donating is a measure of revealed behavior and one that can be verified through the use of administrative records at the individual-level due to FEC reporting requirements. Second, contribution records offer an important way to measure the intensity of preferences by using the amount and frequency of contributions.^[It’s important to note that while contributions provide much more variation, they are not without their limits. Contributions are only required to be recorded at the individual level if the amount is over \$200. This means any amount below \$200 will be categorized under “unitemized contributions”.]  Unlike voting which is a binary measure, contribution records allow for a wide degree of variation in both the total amount given and the frequency of donations which I leverage to measure intensity for co ethnic representatives. Third, donating is not bound by geographical constraints or binary choice constraints. Unlike voting in which voters must choose between two candidates running in their own district, donors are free to give to any candidate, and to amounts that range up to $2,700 per election. 

Finally, one of the reasons why rates of donating are relatively small compared to other acts of political participation is the high barrier to entry, specifically having the resources to make a contribution (i.e. Verba, Schlozman, and Brady 1995; Schlozman, Verba, and Brady 2012; Rosenstone and Hansen 1993). However, the high cost associated with donating also represents increased costs for expressions of coethnic support because the donor is committing valuable resources to particular candidate. This cost stands in stark contrast to studies that rely on self-reported survey data that ask hypothetical scenarios about preferences for co ethnic representation where the respondent incurs no tangible costs in giving their response. Similarly, the cost of donating requires more in the way of resources compared to voting.

In my dissertation, I analyze millions of administrative records along with contextual measures to explore how well Asian American and Latino donors fit conventional expectations for donor behavior. I evaluate the extent to which these groups defy these expectations and give to a co-ethnic/co-racial candidate. I find that under certain circumstances, Asian and Latino donors prefer co-racial candidates, even after controlling for conventional factors. Instead of prioritizing partisanship, ideological and geographical proximity, Asian American and Latino donors are willing to reach across the aisle and across the country to support candidates who share their race or ethnicity.

**What does this mean for the Republican Party and Asian Americans?**

Following the disastrous 2012 election, the Republican Party commissioned the now well-known Growth and Opportunity Project report which outlined vulnerabilities of the Party and recommended steps to grow the Party and improve Republican campaigns moving forward. In terms of the Asian American and Pacific Islander community, the recommendations included promoting and supporting AAPI candidates and developing a “rising star” program at state and local levels to encourage AAPIs to run for elected office. 

In California, it looks as though the GOP is taking these recommendations seriously with recent efforts to win over Asian Americans by supporting AAPI candidates in Orange County in [2014](https://www.ocregister.com/2017/01/23/oc-offers-gop-example-of-asian-outreach/), and expanded outreach to [voters](https://www.scpr.org/blogs/multiamerican/2014/02/10/15800/republican-national-committee-asian-american-voter/).  In short, if Kim’s candidacy is any indication, the path to increasing support from Asian American voters and especially Asian donors is through running more Asian American candidates.




