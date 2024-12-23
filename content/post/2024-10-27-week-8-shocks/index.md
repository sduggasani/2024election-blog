---
title: 'Week 8: Shocks'
author: Sammy Duggasani
date: '2024-10-27'
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

# **Week 8: Shocks**

**Monday, October 28, 2024**\
**7 Days until Presidential Election**

*Can you believe there is just a week left until election day? Thank you for following along throughout this entire process! This will be my second-to-last post, and next week I will post my final prediction. This week we've been learning about October surprises, which refer to unanticipated events that happen in the month before election day that are thought to impact the final results of the race. This week, the Trump campaign held an event at Madison Square Garden where the comedian Tony Hinchcliffe made problematic jokes about Puerto Rico and Latinos, possibly alienating a demographic that has Trump has made headway with this cycle. President Biden made a clumsily-worded response to the event with people construing his words as referring to Trump's supporters as "[garbage](https://www.cbsnews.com/news/bidens-response-to-garbage-joke-about-puerto-rico/)". I also dealt with my own "October surprise" this week after realizing that my absentee ballot that I applied for two weeks ago likely got lost in the mail and that it was too late to request another to my dorm in Cambridge, MA. After finding a flight back home to Atlanta for \$75, I decided it was worth it to cast my ballot in person on election day. Hopefully, everything goes smoothly, and I can participate in the electoral process. Because the impact of shocks are difficult to measure on vote behavior or outcomes, we will use our analysis this week just to update my model and evaluate its results.*





## Updating Model Predictions



This week to update model predictions, I rely on the same inputs as the last few weeks: Democrat 2 Party Vote Shares in the past two elections, latest poll averages for Democrats, mean poll averages for Democrats, Consumer Price Index, quarterly GDP growth, and campaign donations. Realistically, the only thing that has changed between past weeks' models and this week's is polling data. The most recent polling data I include has results from up to 8 days before the election day on November 5th.

## Model Predictions without Regularization

<table class="table table-hover" style="margin-left: auto; margin-right: auto;">
<caption>Table 1: Battleground State Predicted Results for 2024 Without Regularization</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> state </th>
   <th style="text-align:right;"> mean_dem </th>
   <th style="text-align:right;"> sd_dem </th>
   <th style="text-align:right;"> lower_dem </th>
   <th style="text-align:right;"> upper_dem </th>
   <th style="text-align:right;"> mean_rep </th>
   <th style="text-align:right;"> sd_rep </th>
   <th style="text-align:right;"> lower_rep </th>
   <th style="text-align:right;"> upper_rep </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Arizona</span> </td>
   <td style="text-align:right;"> 52.95022 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 52.95022 </td>
   <td style="text-align:right;"> 52.95022 </td>
   <td style="text-align:right;"> 47.04978 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 47.04978 </td>
   <td style="text-align:right;"> 47.04978 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Georgia</span> </td>
   <td style="text-align:right;"> 53.15389 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 53.15389 </td>
   <td style="text-align:right;"> 53.15389 </td>
   <td style="text-align:right;"> 46.84611 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 46.84611 </td>
   <td style="text-align:right;"> 46.84611 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Michigan</span> </td>
   <td style="text-align:right;"> 53.80728 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 53.80728 </td>
   <td style="text-align:right;"> 53.80728 </td>
   <td style="text-align:right;"> 46.19272 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 46.19272 </td>
   <td style="text-align:right;"> 46.19272 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Nevada</span> </td>
   <td style="text-align:right;"> 54.02149 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 54.02149 </td>
   <td style="text-align:right;"> 54.02149 </td>
   <td style="text-align:right;"> 45.97851 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 45.97851 </td>
   <td style="text-align:right;"> 45.97851 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">North Carolina</span> </td>
   <td style="text-align:right;"> 53.05170 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 53.05170 </td>
   <td style="text-align:right;"> 53.05170 </td>
   <td style="text-align:right;"> 46.94830 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 46.94830 </td>
   <td style="text-align:right;"> 46.94830 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Pennsylvania</span> </td>
   <td style="text-align:right;"> 53.31148 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 53.31148 </td>
   <td style="text-align:right;"> 53.31148 </td>
   <td style="text-align:right;"> 46.68852 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 46.68852 </td>
   <td style="text-align:right;"> 46.68852 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Wisconsin</span> </td>
   <td style="text-align:right;"> 53.98853 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 53.98853 </td>
   <td style="text-align:right;"> 53.98853 </td>
   <td style="text-align:right;"> 46.01147 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 46.01147 </td>
   <td style="text-align:right;"> 46.01147 </td>
  </tr>
</tbody>
</table>

Using these inputs, I created a simple prediction of Democratic vote share through a linear regression model; I calculated Republican vote share by subtracting Democratic 2-Party vote share from 100%. This resulted in some pretty obviously problematic findings: that Harris will take all battleground states with a clear lead and miniscule standard deviation that doesn't place the results within the margin of error. This deviates from all credible models and is not something I would trust. So, I will not use these findings for my final forecast.

## LASSO Regression Model

Instead of a simple linear regression, I find it more useful to employ a LASSO Regression model, which will use only those variables with large enough coefficients (or effects on Democrat 2-Party Vote Share) and nullify other small variables. I choose this model because I am incredibly cautious of constructing an overfitted and overly complex model to forecast the election results. Realistically, I am focused on three things: relevant economic indicators, campaign donations, and Democratic performance in polls and past elections.



<table class="table table-hover" style="margin-left: auto; margin-right: auto;">
<caption>Table 2: Battleground State Predicted Results for 2024</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> state </th>
   <th style="text-align:right;"> electors </th>
   <th style="text-align:right;"> Democrat </th>
   <th style="text-align:right;"> Republican </th>
   <th style="text-align:left;"> winner </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Arizona</span> </td>
   <td style="text-align:right;"> 11 </td>
   <td style="text-align:right;"> 49.29145 </td>
   <td style="text-align:right;"> 50.70855 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Georgia</span> </td>
   <td style="text-align:right;"> 16 </td>
   <td style="text-align:right;"> 49.48063 </td>
   <td style="text-align:right;"> 50.51937 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Michigan</span> </td>
   <td style="text-align:right;"> 15 </td>
   <td style="text-align:right;"> 50.18718 </td>
   <td style="text-align:right;"> 49.81282 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Nevada</span> </td>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:right;"> 50.02578 </td>
   <td style="text-align:right;"> 49.97422 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">North Carolina</span> </td>
   <td style="text-align:right;"> 16 </td>
   <td style="text-align:right;"> 49.33849 </td>
   <td style="text-align:right;"> 50.66151 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Pennsylvania</span> </td>
   <td style="text-align:right;"> 19 </td>
   <td style="text-align:right;"> 49.86543 </td>
   <td style="text-align:right;"> 50.13457 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Wisconsin</span> </td>
   <td style="text-align:right;"> 10 </td>
   <td style="text-align:right;"> 50.34243 </td>
   <td style="text-align:right;"> 49.65757 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
</tbody>
</table>

The results of using LASSO regression are a bit more believable, showing some battleground states going to Harris and most to Trump. The split of battleground states also comports well with what other models are predicting and my general intuition. I would be apprehensive about the exact point estimates of Democrat and Republican vote shares, but I think generally the winner for each state makes sense. Now, let's take these results, fit them within the context of the whole nation, and see who is predicted to win the electoral college next week.

<table class="table table-hover" style="margin-left: auto; margin-right: auto;">
<caption>Table 3: Predicted Electoral Votes by State for 2024</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> State </th>
   <th style="text-align:right;"> Predicted Electoral Votes </th>
   <th style="text-align:left;"> Winner </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Alabama</span> </td>
   <td style="text-align:right;"> 9 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Alaska</span> </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Arizona</span> </td>
   <td style="text-align:right;"> 11 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Arkansas</span> </td>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">California</span> </td>
   <td style="text-align:right;"> 54 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Colorado</span> </td>
   <td style="text-align:right;"> 10 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Connecticut</span> </td>
   <td style="text-align:right;"> 7 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Delaware</span> </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">District Of Columbia</span> </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Florida</span> </td>
   <td style="text-align:right;"> 30 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Georgia</span> </td>
   <td style="text-align:right;"> 16 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Hawaii</span> </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Idaho</span> </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Illinois</span> </td>
   <td style="text-align:right;"> 19 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Indiana</span> </td>
   <td style="text-align:right;"> 11 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Iowa</span> </td>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Kansas</span> </td>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Kentucky</span> </td>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Louisiana</span> </td>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Maine</span> </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Maryland</span> </td>
   <td style="text-align:right;"> 10 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Massachusetts</span> </td>
   <td style="text-align:right;"> 11 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Michigan</span> </td>
   <td style="text-align:right;"> 15 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Minnesota</span> </td>
   <td style="text-align:right;"> 10 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Mississippi</span> </td>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Missouri</span> </td>
   <td style="text-align:right;"> 10 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Montana</span> </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Nebraska</span> </td>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Nevada</span> </td>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">New Hampshire</span> </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">New Jersey</span> </td>
   <td style="text-align:right;"> 14 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">New Mexico</span> </td>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">New York</span> </td>
   <td style="text-align:right;"> 28 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">North Carolina</span> </td>
   <td style="text-align:right;"> 16 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">North Dakota</span> </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Ohio</span> </td>
   <td style="text-align:right;"> 17 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Oklahoma</span> </td>
   <td style="text-align:right;"> 7 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Oregon</span> </td>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Pennsylvania</span> </td>
   <td style="text-align:right;"> 19 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Rhode Island</span> </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">South Carolina</span> </td>
   <td style="text-align:right;"> 9 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">South Dakota</span> </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Tennessee</span> </td>
   <td style="text-align:right;"> 11 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Texas</span> </td>
   <td style="text-align:right;"> 40 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Utah</span> </td>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Vermont</span> </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Virginia</span> </td>
   <td style="text-align:right;"> 13 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Washington</span> </td>
   <td style="text-align:right;"> 12 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">West Virginia</span> </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Wisconsin</span> </td>
   <td style="text-align:right;"> 10 </td>
   <td style="text-align:left;"> Democrat </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Wyoming</span> </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:left;"> Republican </td>
  </tr>
</tbody>
</table>

<table class="table table-hover" style="margin-left: auto; margin-right: auto;">
<caption>Table 3: Predicted Electoral Votes for 2024</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> Winner </th>
   <th style="text-align:right;"> Electoral Votes </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Democrat</span> </td>
   <td style="text-align:right;"> 257 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style=" font-weight: bold;    color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Republican</span> </td>
   <td style="text-align:right;"> 281 </td>
  </tr>
</tbody>
</table>

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-1.png" width="672" />

In previous weeks, I took certain states as "red" states and others as "blue" states based on my intuition and without much justification. The purpose of this was to predict only for battleground states because all other states' electoral votes were assumed to go to Harris or Trump. I should have defended this assumption, so this week, I am updating my model to use the party winner of the state in 2020 for all states except for the battleground states (instead of just casting certain states as Republican or Democratic givens).

After doing this, I find my model predicts that the Republicans will take the White House in November, having won all the non-battleground states they did in 2020 and taking Arizona, Georgia, North Carolina, and Pennsylvania. This means that, between 2020 and 2024, the Democrats would have lost Arizona, Georgia, and Pennsylvania.

Looking at the map, we can see that the South once again is predicted to vote as a Republican bloc, the Northeast and West Coast remain Democratic strongholds, and the Rust Belt states split down the middle.

## Conclusion

**According to this week's model, Trump will win the 2024 Presidential Election, taking 281 electoral votes.**

In comparison to last week's model, this week presents a more tempered victory for Trump. I made an effort to regularize my model this week through LASSO this week because I want to be as conservative as possible about introducing new variables into my model, and I think that is mainly why this week's model presents a much much tighter margin. Still, this favors Trump compared to the last time I used LASSO regression because of most recent polling data. In my final prediction, I will continue to rely on this structure and regularize my model with LASSO. It is important to note that the margin of error straddles the win threshold, so these predictions can really go either way to Trump or Harris. Realistically, no one should be surprised by the winner of the election because this race is so close.

## Sources

"'Supporters" or "supporter's'? Biden comments about Trump 'garbage' rally anger the GOP" *CBS News*, 2024. <https://www.cbsnews.com/news/bidens-response-to-garbage-joke-about-puerto-rico/>.

Polling Data Provided by GOV 1347: Election Analytics teaching staff (which drew from the FiveThirtyEight GitHub)

Economic Data Provided by GOV 1347: Election Analytics teaching staff (which drew from the Bureau of Economic Analysis and Federal Reserve Economic Data)
