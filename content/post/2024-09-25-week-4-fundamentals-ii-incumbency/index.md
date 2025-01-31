---
title: 'Week 4: Fundamentals II, Incumbency'
author: Sammy Duggasani
date: '2024-09-25'
slug: []
categories: []
tags: []
---
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />

# **Week 4: Fundamentals II, Incumbency**

**Monday, September 30, 2024**\
**35 Days until Presidential Election**

*Today marks about a month since I've started this blog to follow and forecast the 2024 Presidential Election. Thanks for following along!*

*After two assassination attempts, the presence of Security Service at Trump's rallies has become a point of attack for his campaign. Most recently, he has [blamed the Biden administration](https://newrepublic.com/post/186504/donald-trump-joe-biden-theory-crowd-sizes) for withholding personnel to guard his events, thereby hindering them from reaching the size they once did. The powers that incumbent political candidates have an don't have is a large focus of American political science. While I am skeptical that we can group Trump's rally attendance in with incumbent advantage, we should scrutinize how the theory applies to this year's election—especially in relation to who we actually consider to be the incumbent between Harris and Trump.*





## Descriptive Statistics on Incumbent Advantage

<table class="table table-hover" style="margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> Incumbent President Re-elected </th>
   <th style="text-align:right;"> Count </th>
   <th style="text-align:right;"> Percentage </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:right;"> 12 </td>
   <td style="text-align:right;"> 66.67 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> TRUE </td>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:right;"> 33.33 </td>
  </tr>
</tbody>
</table>

```
## Elections with At Least One Incumbent Running: 11
## Incumbent Victories: 7
## Percentage: 63.64
```

<table class="table table-hover" style="margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:right;"> Election Year </th>
   <th style="text-align:left;"> Democratic Candidate </th>
   <th style="text-align:left;"> Republican Candidate </th>
   <th style="text-align:left;"> Democratic Incumbency </th>
   <th style="text-align:left;"> Republican Incumbency </th>
   <th style="text-align:left;"> Democratic Win </th>
   <th style="text-align:left;"> Republican Win </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 2004 </td>
   <td style="text-align:left;"> Kerry, John </td>
   <td style="text-align:left;"> Bush, George W. </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> TRUE </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> TRUE </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012 </td>
   <td style="text-align:left;"> Obama, Barack H. </td>
   <td style="text-align:left;"> Romney, Mitt </td>
   <td style="text-align:left;"> TRUE </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> TRUE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2020 </td>
   <td style="text-align:left;"> Biden, Joseph R. </td>
   <td style="text-align:left;"> Trump, Donald J. </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> TRUE </td>
   <td style="text-align:left;"> TRUE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
</tbody>
</table>

<table class="table table-hover" style="margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> Incumbent Party Re-elected </th>
   <th style="text-align:right;"> Count </th>
   <th style="text-align:right;"> Percentage </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:right;"> 10 </td>
   <td style="text-align:right;"> 55.56 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> TRUE </td>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:right;"> 44.44 </td>
  </tr>
</tbody>
</table>

<table class="table table-hover" style="margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> Previous Administration Member Elected </th>
   <th style="text-align:right;"> Percentage </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:right;"> 72.22 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> TRUE </td>
   <td style="text-align:right;"> 27.78 </td>
  </tr>
</tbody>
</table>

Above we calculate some descriptive statistics on the incumbency advantage. If we simply look at the number of times an incumbent president is reelected or the number of times an incumbent party is reelected, it looks like incumbents actually have worse chances at being elected into office for a second time. Let us actually consider those elections which have incumbent running, however, and we see that incumbents have a higher rate of winning elections than non-incumbents.

## Pork Barrel Spending and Incumbency

The advantage of incumbents is partly attributed to the powers they hold while in office and the ability to leverage them to garner votes. One such power is the power to apportion federal spending monies to key certain constituencies; this is known as pork barrel spending. The function of pork barrel spending lies in the idea that voters who receive more funding from an incumbent administration are more likely to view that administration favorably and cast their votes for them in the next election.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" /><img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-2.png" width="672" /><table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>Table 1: Pork County-Level Model</caption>
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:center;"> Model 1 </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> (Intercept) </td>
   <td style="text-align:center;"> −6.450 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.084) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dpct_grants </td>
   <td style="text-align:center;"> 0.005 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.001) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> comp_state </td>
   <td style="text-align:center;"> 0.153 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.076) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> as.factor(year)1992 </td>
   <td style="text-align:center;"> 0.171 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.116) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> as.factor(year)1996 </td>
   <td style="text-align:center;"> 6.345 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.116) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> as.factor(year)2000 </td>
   <td style="text-align:center;"> −2.050 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.116) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> as.factor(year)2004 </td>
   <td style="text-align:center;"> 8.407 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.116) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> as.factor(year)2008 </td>
   <td style="text-align:center;"> 3.137 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.116) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dpct_grants × comp_state </td>
   <td style="text-align:center;"> 0.006 </td>
  </tr>
  <tr>
   <td style="text-align:left;box-shadow: 0px 1px">  </td>
   <td style="text-align:center;box-shadow: 0px 1px"> (0.002) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Num.Obs. </td>
   <td style="text-align:center;"> 18464 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> R2 </td>
   <td style="text-align:center;"> 0.403 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> R2 Adj. </td>
   <td style="text-align:center;"> 0.402 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> AIC </td>
   <td style="text-align:center;"> 107912.7 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> BIC </td>
   <td style="text-align:center;"> 107990.9 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Log.Lik. </td>
   <td style="text-align:center;"> −53946.355 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> F </td>
   <td style="text-align:center;"> 1555.616 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> RMSE </td>
   <td style="text-align:center;"> 4.49 </td>
  </tr>
</tbody>
</table>

<table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>Table 1: Extended Pork County-Level Model</caption>
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:center;"> Model 1 </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> (Intercept) </td>
   <td style="text-align:center;"> −6.523 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.085) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dpct_grants </td>
   <td style="text-align:center;"> 0.004 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.001) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> comp_state </td>
   <td style="text-align:center;"> 0.155 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.077) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> as.factor(year)1992 </td>
   <td style="text-align:center;"> −0.156 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.121) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> as.factor(year)1996 </td>
   <td style="text-align:center;"> 6.231 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.120) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> as.factor(year)2000 </td>
   <td style="text-align:center;"> −2.000 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.119) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> as.factor(year)2004 </td>
   <td style="text-align:center;"> 8.248 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.119) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> as.factor(year)2008 </td>
   <td style="text-align:center;"> 3.574 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.124) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dpc_income </td>
   <td style="text-align:center;"> 0.134 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.022) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> inc_ad_diff </td>
   <td style="text-align:center;"> 0.061 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.011) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> inc_campaign_diff </td>
   <td style="text-align:center;"> 0.162 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.013) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dhousevote_inc </td>
   <td style="text-align:center;"> 0.012 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.002) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> iraq_cas2004 </td>
   <td style="text-align:center;"> −0.153 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.070) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> iraq_cas2008 </td>
   <td style="text-align:center;"> −0.165 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.022) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dpct_popl </td>
   <td style="text-align:center;"> 2.103 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.530) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dpct_grants × comp_state </td>
   <td style="text-align:center;"> 0.006 </td>
  </tr>
  <tr>
   <td style="text-align:left;box-shadow: 0px 1px">  </td>
   <td style="text-align:center;box-shadow: 0px 1px"> (0.002) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Num.Obs. </td>
   <td style="text-align:center;"> 17959 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> R2 </td>
   <td style="text-align:center;"> 0.420 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> R2 Adj. </td>
   <td style="text-align:center;"> 0.419 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> AIC </td>
   <td style="text-align:center;"> 104624.8 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> BIC </td>
   <td style="text-align:center;"> 104757.3 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Log.Lik. </td>
   <td style="text-align:center;"> −52295.398 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> F </td>
   <td style="text-align:center;"> 865.892 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> RMSE </td>
   <td style="text-align:center;"> 4.45 </td>
  </tr>
</tbody>
</table>

<table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>Table 1: Pork State-Level Model</caption>
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:center;"> Model 1 </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> (Intercept) </td>
   <td style="text-align:center;"> 9.635 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (3.632) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> is_comp </td>
   <td style="text-align:center;"> −0.400 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (4.150) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> change_grant_mil </td>
   <td style="text-align:center;"> 0.114 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.105) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> as.factor(year)1992 </td>
   <td style="text-align:center;"> 6.895 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (6.717) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> as.factor(year)1996 </td>
   <td style="text-align:center;"> −21.379 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (5.273) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> as.factor(year)2000 </td>
   <td style="text-align:center;"> 3.577 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (5.626) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> as.factor(year)2004 </td>
   <td style="text-align:center;"> −30.162 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (5.475) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> as.factor(year)2008 </td>
   <td style="text-align:center;"> 1.085 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (4.863) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> is_comp × change_grant_mil </td>
   <td style="text-align:center;"> −0.103 </td>
  </tr>
  <tr>
   <td style="text-align:left;box-shadow: 0px 1px">  </td>
   <td style="text-align:center;box-shadow: 0px 1px"> (0.164) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Num.Obs. </td>
   <td style="text-align:center;"> 300 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> R2 </td>
   <td style="text-align:center;"> 0.268 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> R2 Adj. </td>
   <td style="text-align:center;"> 0.247 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> AIC </td>
   <td style="text-align:center;"> 2754.6 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> BIC </td>
   <td style="text-align:center;"> 2791.6 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Log.Lik. </td>
   <td style="text-align:center;"> −1367.285 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> F </td>
   <td style="text-align:center;"> 13.286 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> RMSE </td>
   <td style="text-align:center;"> 23.07 </td>
  </tr>
</tbody>
</table>

Here, we visualize a replication of the findings from Kriner and Reeves' "Presidential Particularism and Divide-the-Dollar Politics" (2015). They find that spending of federal grants in swing states is higher than core states. Just looking at swing states, there is a sizable difference in spending when an incumbent is running in an election versus when they are not. It is intuitive that incumbents use federal spending to advantage them in upcoming elections when they have them. My hope is that visualizing pork barrel spending can help give shape to the idea of the incumbency advantage.

## Time for a Change Model

One model of the incumbency advantage is Alan Abramowitz's **Time for Change** model, which he developed in 1988. It is a simple Ordinary Least Squares Regression Model that relies on three independent variables: GDP Growth for Quarter 2, June Gallup Poll Approval, and a binary variable on incumbency status of a candidate.

<table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>Table 2: Time for Change Models for 2024</caption>
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:center;"> Excluding 2020 Data </th>
   <th style="text-align:center;"> Including 2020 Data </th>
   <th style="text-align:center;"> Harris Non-Incumbent Hypothetical, Excluding 2020 </th>
   <th style="text-align:center;"> Harris Non-Incumbent Hypothetical, Including 2020 </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> (Intercept) </td>
   <td style="text-align:center;"> 48.212 </td>
   <td style="text-align:center;"> 49.236 </td>
   <td style="text-align:center;"> 48.212 </td>
   <td style="text-align:center;"> 49.236 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (1.070) </td>
   <td style="text-align:center;"> (1.117) </td>
   <td style="text-align:center;"> (1.070) </td>
   <td style="text-align:center;"> (1.117) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> GDP Growth (Quarterly) </td>
   <td style="text-align:center;"> 0.465 </td>
   <td style="text-align:center;"> 0.147 </td>
   <td style="text-align:center;"> 0.465 </td>
   <td style="text-align:center;"> 0.147 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (0.155) </td>
   <td style="text-align:center;"> (0.088) </td>
   <td style="text-align:center;"> (0.155) </td>
   <td style="text-align:center;"> (0.088) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Incumbency Status </td>
   <td style="text-align:center;"> 2.220 </td>
   <td style="text-align:center;"> 2.576 </td>
   <td style="text-align:center;"> 2.220 </td>
   <td style="text-align:center;"> 2.576 </td>
  </tr>
  <tr>
   <td style="text-align:left;">  </td>
   <td style="text-align:center;"> (1.244) </td>
   <td style="text-align:center;"> (1.411) </td>
   <td style="text-align:center;"> (1.244) </td>
   <td style="text-align:center;"> (1.411) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Approval Rating in June </td>
   <td style="text-align:center;"> 0.132 </td>
   <td style="text-align:center;"> 0.139 </td>
   <td style="text-align:center;"> 0.132 </td>
   <td style="text-align:center;"> 0.139 </td>
  </tr>
  <tr>
   <td style="text-align:left;box-shadow: 0px 1px">  </td>
   <td style="text-align:center;box-shadow: 0px 1px"> (0.025) </td>
   <td style="text-align:center;box-shadow: 0px 1px"> (0.029) </td>
   <td style="text-align:center;box-shadow: 0px 1px"> (0.025) </td>
   <td style="text-align:center;box-shadow: 0px 1px"> (0.029) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Num.Obs. </td>
   <td style="text-align:center;"> 18 </td>
   <td style="text-align:center;"> 19 </td>
   <td style="text-align:center;"> 18 </td>
   <td style="text-align:center;"> 19 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> R2 </td>
   <td style="text-align:center;"> 0.817 </td>
   <td style="text-align:center;"> 0.753 </td>
   <td style="text-align:center;"> 0.817 </td>
   <td style="text-align:center;"> 0.753 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> R2 Adj. </td>
   <td style="text-align:center;"> 0.777 </td>
   <td style="text-align:center;"> 0.703 </td>
   <td style="text-align:center;"> 0.777 </td>
   <td style="text-align:center;"> 0.703 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> AIC </td>
   <td style="text-align:center;"> 89.3 </td>
   <td style="text-align:center;"> 99.1 </td>
   <td style="text-align:center;"> 89.3 </td>
   <td style="text-align:center;"> 99.1 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> BIC </td>
   <td style="text-align:center;"> 93.8 </td>
   <td style="text-align:center;"> 103.8 </td>
   <td style="text-align:center;"> 93.8 </td>
   <td style="text-align:center;"> 103.8 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Log.Lik. </td>
   <td style="text-align:center;"> −39.673 </td>
   <td style="text-align:center;"> −44.548 </td>
   <td style="text-align:center;"> −39.673 </td>
   <td style="text-align:center;"> −44.548 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> F </td>
   <td style="text-align:center;"> 20.783 </td>
   <td style="text-align:center;"> 15.217 </td>
   <td style="text-align:center;"> 20.783 </td>
   <td style="text-align:center;"> 15.217 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> RMSE </td>
   <td style="text-align:center;"> 2.19 </td>
   <td style="text-align:center;"> 2.52 </td>
   <td style="text-align:center;"> 2.19 </td>
   <td style="text-align:center;"> 2.52 </td>
  </tr>
</tbody>
</table>

<table class="table table-hover" style="margin-left: auto; margin-right: auto;">
<caption>Table 2: Two-Party Vote Shares (%) Across Various Time for Change Models</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> Candidate </th>
   <th style="text-align:left;"> Excluding 2020 Data </th>
   <th style="text-align:left;"> Including 2020 Data </th>
   <th style="text-align:left;"> Harris Non-Incumbent Hypothetical, Excluding 2020 </th>
   <th style="text-align:left;"> Harris Non-Incumbent Hypothetical, Including 2020 </th>
   <th style="text-align:left;"> Silver's Ensemble Model, Weighing Polls Closer to Election Day </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Kamala Harris </td>
   <td style="text-align:left;"> 48.93 </td>
   <td style="text-align:left;"> 49.2 </td>
   <td style="text-align:left;"> 46.71 </td>
   <td style="text-align:left;"> 46.62 </td>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">51.31</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Donald Trump </td>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">51.07</span> </td>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">50.8</span> </td>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">53.29</span> </td>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">53.38</span> </td>
   <td style="text-align:left;"> 48.07 </td>
  </tr>
</tbody>
</table>

I have constructed four models based off of Abramowitz's Time for Change theory and predicted the upcoming 2024 election. In two models, I treat Harris as an incumbent candidate (and Trump a non-incumbent) and the other two models, I treat both candidates as non-incumbents. Like in previous weeks, I have compare models that include 2020 as a data point on which I train the model.

All models show promise with relatively high R-squared and adjusted-R-squared values. For the very first time since I have started this blog, a model I constructed predicted a Trump win in popular vote. In fact, across all Time for Change models, Trump is predicted to win the popular vote—whether or not I include 2020 training data and whether I not I treat Harris as an incumbent candidate. We can see how this differs from my preferred model thus far constructed: Nate Silver's, which is an ensemble model that involves economic and polling data and weighs polls higher the closer they get to election day (See more on this in Week 3's blog post).

All this to say, the predicted two-party vote shares predicted from Abramowitz's model shows a difference when we treat Harris as an incumbent and when we do not. This makes sense as we would expect an incumbent to be advantaged by some number of percentage points than they would otherwise.

## Conclusion

**Trump is predicted to win the popular vote in November.**

Across all four models I constructed off of Abramowitz's Time for Change Model, Donald Trump is predicted to have a greater-than-one-point lead over Harris in two-party popular vote share. This is the first time that Trump has been predicted to win in my models. When Harris's incumbent advantage is removed, his lead over her widens.

## **Sources**

Abramowitz, Alan I. “An Improved Model for Predicting Presidential Election Outcomes.” *PS: Political Science and Politics*, vol. 21, no. 4, 1988, pp. 843–47. JSTOR, <https://doi.org/10.2307/420023>.

Kriner, Douglas L., and Andrew Reeves. “Presidential Particularism and Divide-the-Dollar Politics.” *American Political Science Review* 109.1 (2015): 155–171. Web.

Olmsted, Edith. “Trump Has a Wild New Theory for His Flagging Crowd Sizes.” *The New Republic*, 30 Sept. 2024, <https://newrepublic.com/post/186504/donald-trump-joe-biden-theory-crowd-sizes.>

“When and Where Is the Vance-Walz US Vice Presidential Debate?” *Reuters*, 19 Sept. 2024, [www.reuters.com/world/us/when-where-is-vance-walz-us-vice-presidential-debate-2024-09-19/](http://www.reuters.com/world/us/when-where-is-vance-walz-us-vice-presidential-debate-2024-09-19/).

Polling Data Provided by GOV 1347: Election Analytics teaching staff (which itself drew from the FiveThirtyEight GitHub)

Economic Data Provided by GOV 1347: Election Analytics teaching staff (which itself drew from the Burueau of Economic Analysia and Federal Reserve Economic Data)
