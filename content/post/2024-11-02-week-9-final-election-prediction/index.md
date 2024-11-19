---
title: 'Week 9: Final Election Prediction'
author: Sammy Duggasani
date: '2024-11-02'
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

# **Week 9: Final Prediction**

**Monday, November 4, 2024**\
**1 Day until Presidential Election**

*Election Day is tomorrow! I'm flying to Atlanta Tuesday morning and immediately heading to my polling station to cast my ballot after having a lot of trouble with the mail-in process. When I began this blog nine weeks ago, I had very little knowledge of the inner-workings of election forecasting and the kind of data that was fed into predictive electoral models. Over the course of the past two months, I have built models using simple linear regression, probabilistic models, and machine learning methods — all of which had varying levels of robustness and reliability. Some had predicted a Harris landslide, others heavily favored Trump. In the past few weeks, though, my selection of a singular model type and efforts toward regularization have converged the forecasts on an incredibly tight race between the two candidates. As any major forecaster will tell you, this election can go either way. The purpose of this blog post is to corroborate this idea and to make one final prediction before we begin to see results unfold tomorrow ([and likely over the course of this week](https://globalnews.ca/news/10834744/us-election-results-when-will-we-know/)).*







## Model Description & Coefficients


```
## Warning: Option grouped=FALSE enforced in cv.glmnet, since < 3 observations per
## fold
```

For my final election prediction model, I decided to go with a LASSO regression. Throughout this semester, we have looked at a number of predictors that could have an impact on a presidential candidate's vote share — from economic indicators to polling data to demographics to hurricanes and other shocks. With all these inputs in mind, I thought it most useful to find a method that selects only the most significant or useful features. This is the function of LASSO, which nullifies those predictors that are not as influential on the response variable. A lot of election forecasts run the risk of overfitting because they take in too much information and generate patterns of out of data that does not necessarily reflect reality. I thought it would be better to be conservative with selecting predictors and LASSO regression helped me do that.



Here, you can see the predictors and data that I decided to include in my LASSO regression model. I converged on these variables throughout the weeks by testing each of their relationships with a response variable of Democratic 2-party vote share. I included only those predictors which a significant impact on vote share: this includes a state's voting behavior in past elections, state polling data, economic indicators, and campaign donation data. After having cross-validated to find the ideal lambda value for my LASSO regression, my model has nullified the Mean Democratic Poll Average variable. So, my final regularized model has corrected for a variable that I included, which might not actually have been that informative despite my previous regressions.

![Model Formula](images/Screenshot%202024-11-04%20at%203.57.10%20PM.png)

![LASSO Regularization Objective Formula](images/Screenshot%202024-11-04%20at%203.57.07%20PM.png)

The first is the formula representation of my predictive model, where y refers to Democratic 2-Party Vote Share for a given state in a given election year. The second is a mathematical representation of the regularization objective that would occur for these predictors in particular.

To interpret the coefficients as they are represented above, we can say that, if a Democratic party were to receive 0% of the vote in the past two elections, the latest polling average for Democrats is 0, the Consumer Price Index is 0, there is no GDP growth for quarter 2 that year, and there are no campaign donations for the candidate, then the Democrat running that year in that state would get about 7.7% of the 2-Party vote share. Holding all other variables constant, as the Democratic vote share in the past election increases by a point so does the Democratic vote share in the upcoming election by .1257 points (and .0079 points with respect to a point increase in Democratic vote share in the second-to-last election). Holding all other variables constant, a point increase in the latest polling average for Democrats coincides with about a .98 point increase in Democratic 2-Party vote share in the upcoming election. Holding all other variables constant, a point increase in GDP Growth in Quarter 2 results in a .06 point increase in Democratic 2-Party vote share in the upcoming election. Finally, holding all other variables constant, a point increase in the log of campaign donations to Democrats results in about a .6 point decrease in the Democratic 2-party vote share in the upcoming election. All these coefficients seem intuitive except for the campaign donation variable. This representation is due to the logarithmic transformation of campaign donation data to scale its coefficient, but in reality, there exists a positive relationship between how much money a Democratic campaign rakes in and its eventual vote share. ([Refer to Week 6's blog for more on this.](https://sduggasani.github.io/2024election-blog/post/2024-10-12-week-6-campaign-spending/))


```
## Loading required package: Matrix
```

```
## 
## Attaching package: 'Matrix'
```

```
## The following objects are masked from 'package:tidyr':
## 
##     expand, pack, unpack
```

```
## Loaded glmnet 4.1-6
```

<table class="table table-striped" style="margin-left: auto; margin-right: auto;">
<caption>Table 1: (\#tab:unnamed-chunk-5)Coefficients about a 95% Confidence Interval</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> Predictor </th>
   <th style="text-align:right;"> Lower </th>
   <th style="text-align:right;"> Upper </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> (Intercept) </td>
   <td style="text-align:right;"> -37.0735241 </td>
   <td style="text-align:right;"> 50.2256605 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> D_pv2p_lag1 </td>
   <td style="text-align:right;"> 0.0000000 </td>
   <td style="text-align:right;"> 0.4574302 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> D_pv2p_lag2 </td>
   <td style="text-align:right;"> -0.1224704 </td>
   <td style="text-align:right;"> 0.1576207 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> latest_pollav_DEM </td>
   <td style="text-align:right;"> 0.4120334 </td>
   <td style="text-align:right;"> 1.5727115 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> mean_pollav_DEM </td>
   <td style="text-align:right;"> -0.6909748 </td>
   <td style="text-align:right;"> 0.3996177 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> CPI </td>
   <td style="text-align:right;"> -0.1254901 </td>
   <td style="text-align:right;"> 0.1407011 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> GDP_growth_quarterly </td>
   <td style="text-align:right;"> -0.0994109 </td>
   <td style="text-align:right;"> 0.2102683 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> log(contribution_receipt_amount) </td>
   <td style="text-align:right;"> -1.7544576 </td>
   <td style="text-align:right;"> 0.3380642 </td>
  </tr>
</tbody>
</table>

After bootstrapping the LASSO regression, we get the above range of coefficient values within a 95% confidence interval. It is peculiar that a lot of these predictors include 0 in their confidence intervals, which is troublesome for how much value we place on their significance. Nevertheless, their contributions to the model are still valuable to some extent. I will note, however, that the latest polling average for Democrat variable seems to be the most significant and that is reflected in its confidence interval (which does not include 0) and its large coefficient compared to other predictors.

## Model Validation

<table class="table table-striped" style="margin-left: auto; margin-right: auto;">
<caption>Table 3: (\#tab:unnamed-chunk-6)Model Validation Metrics</caption>
 <thead>
  <tr>
   <th style="text-align:left;">  </th>
   <th style="text-align:right;"> Value </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> R Squared </td>
   <td style="text-align:right;"> 0.8563942 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Mean Squared Error </td>
   <td style="text-align:right;"> 1.5842029 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Leave-One-Out Cross-Validation MSE </td>
   <td style="text-align:right;"> 2.7810769 </td>
  </tr>
</tbody>
</table>

To evaluate the robustness of my model, I rely on various model validation methods. First, I made sure to employ cross-validation within my LASSO regression, which minimizes the lambda squared error.

For in sample evaluation, I rely on R-Squared metrics and Mean Squared Error. For the coefficient of determination (R-Squared), I get about .86 which suggests a strong model. The Mean Squared Error is also relatively smalled compared to other models I have constructed in previous weeks. It is by no means small, though, especially considering that an MSE of this value in certain tight races could mean that a race swings either way.

For out of sample evaluation, I also rely on leave-one-out cross-validation. This gives me a higher value than the MSE, which is not the best but can be attributed to the small amount of observations that are used for this model. Realistically, there is not much data to work with for presidential elections, especially where economic indicators, demographics, and campaign donations are concerned. This is a constraint of all election forecasting models, and mine is not immune to it either.

## Uncertainty

<table class="table table-striped" style="margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> State </th>
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
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Arizona</span> </td>
   <td style="text-align:right;"> 49.82247 </td>
   <td style="text-align:right;"> 1.249856 </td>
   <td style="text-align:right;"> 47.37275 </td>
   <td style="text-align:right;"> 52.27219 </td>
   <td style="text-align:right;"> 50.17753 </td>
   <td style="text-align:right;"> 1.249856 </td>
   <td style="text-align:right;"> 47.72781 </td>
   <td style="text-align:right;"> 52.62725 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Georgia</span> </td>
   <td style="text-align:right;"> 49.83683 </td>
   <td style="text-align:right;"> 1.254854 </td>
   <td style="text-align:right;"> 47.37731 </td>
   <td style="text-align:right;"> 52.29634 </td>
   <td style="text-align:right;"> 50.16317 </td>
   <td style="text-align:right;"> 1.254854 </td>
   <td style="text-align:right;"> 47.70366 </td>
   <td style="text-align:right;"> 52.62269 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Michigan</span> </td>
   <td style="text-align:right;"> 50.62857 </td>
   <td style="text-align:right;"> 1.298490 </td>
   <td style="text-align:right;"> 48.08353 </td>
   <td style="text-align:right;"> 53.17361 </td>
   <td style="text-align:right;"> 49.37143 </td>
   <td style="text-align:right;"> 1.298490 </td>
   <td style="text-align:right;"> 46.82639 </td>
   <td style="text-align:right;"> 51.91647 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Nevada</span> </td>
   <td style="text-align:right;"> 50.93553 </td>
   <td style="text-align:right;"> 1.256353 </td>
   <td style="text-align:right;"> 48.47308 </td>
   <td style="text-align:right;"> 53.39799 </td>
   <td style="text-align:right;"> 49.06447 </td>
   <td style="text-align:right;"> 1.256353 </td>
   <td style="text-align:right;"> 46.60201 </td>
   <td style="text-align:right;"> 51.52692 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">North Carolina</span> </td>
   <td style="text-align:right;"> 49.77338 </td>
   <td style="text-align:right;"> 1.336243 </td>
   <td style="text-align:right;"> 47.15435 </td>
   <td style="text-align:right;"> 52.39242 </td>
   <td style="text-align:right;"> 50.22662 </td>
   <td style="text-align:right;"> 1.336243 </td>
   <td style="text-align:right;"> 47.60758 </td>
   <td style="text-align:right;"> 52.84565 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Pennsylvania</span> </td>
   <td style="text-align:right;"> 50.11565 </td>
   <td style="text-align:right;"> 1.238461 </td>
   <td style="text-align:right;"> 47.68827 </td>
   <td style="text-align:right;"> 52.54303 </td>
   <td style="text-align:right;"> 49.88435 </td>
   <td style="text-align:right;"> 1.238461 </td>
   <td style="text-align:right;"> 47.45697 </td>
   <td style="text-align:right;"> 52.31173 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Wisconsin</span> </td>
   <td style="text-align:right;"> 51.04669 </td>
   <td style="text-align:right;"> 1.292186 </td>
   <td style="text-align:right;"> 48.51400 </td>
   <td style="text-align:right;"> 53.57938 </td>
   <td style="text-align:right;"> 48.95331 </td>
   <td style="text-align:right;"> 1.292186 </td>
   <td style="text-align:right;"> 46.42062 </td>
   <td style="text-align:right;"> 51.48600 </td>
  </tr>
</tbody>
</table>

Just like I bootstrapped for my coefficients in the model, I am also bootstrapping for the Democratic 2-Party Vote Share for the battleground states to give more color to the uncertainty around my predictions. For every single swing state, the margin by which the predicted party "wins" is well within the standard deviation, or margin of error. This suggests that, while I am converging on one party to win for a given swing state, they are all toss-ups and either party can realistically win them. That is, my model is not determinative. Still, I place some trust in the mean_dem and mean_rep vote share predictions for the swing states above for the sake of this endeavor and my work of the past few weeks. The states colored in blue are those where the point prediction for Democrats (with 2-Party vote share) is higher than it is for Republicans. The states colored in red are those where the point prediction for Republicans (with 2-Party vote share) is higher than it is for Democrats. The standard deviations for all swing states is relatively the same.

## Electoral College Visualization

<table class="table table-hover" style="margin-left: auto; margin-right: auto;">
<caption>Table 5: Predicted Electoral Votes by State for 2024</caption>
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
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Pennsylvania</span> </td>
   <td style="text-align:right;"> 19 </td>
   <td style="text-align:left;"> Democrat </td>
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
<caption>Table 5: Predicted Electoral Votes for 2024</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> Winner </th>
   <th style="text-align:right;"> Electoral Votes </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> <span style=" font-weight: bold;    color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(79, 148, 205, 255) !important;">Democrat</span> </td>
   <td style="text-align:right;"> 276 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="     color: white !important;border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: rgba(205, 79, 57, 255) !important;">Republican</span> </td>
   <td style="text-align:right;"> 262 </td>
  </tr>
</tbody>
</table>

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-8-1.png" width="672" />

Putting my bootstrapped point predictions into play, I have constructed a final electoral college prediction above. Of the swing states, the Republicans are expected to take Georgia (my home state), North Carolina, and Arizona. The Democrats are expected to take Pennsylvania, Wisconsin, Nevada, and Michigan. This puts the Democrats just barely over the 270 needed to win the office. If this prediction were true, it would make the 2024 election one of the closest in recent history, second only to the 2000 election between Bush and Gore.


## Conclusion

**According to this week's model, Harris will win the 2024 Presidential Election, taking 276 electoral votes.**

My models for the past few weeks have been wavering between a Harris victory and a Trump victory by incredibly close margins. This is an incredibly close race, and we should not be surprised by the results. Thank you for following along for the past couple of weeks. Thank you to the GOV 1347 teaching staff for their help throughout the semester with content questions and technical difficulties. Thank you in particular to Matthew Dardet for all his guidance and Prof. Ryan Enos for his incredibly insightful lectures. Hopefully soon, we will see how my prediction fares. Until then, take care!

## Sources

"US Election Results: When Will We Know?" Global News, 4 Nov. 2024, <https://globalnews.ca/news/10834744/us-election-results-when-will-we-know/>.

Polling Data Provided by GOV 1347: Election Analytics teaching staff (which drew from the FiveThirtyEight GitHub)

Economic Data Provided by GOV 1347: Election Analytics teaching staff (which drew from the Bureau of Economic Analysis and Federal Reserve Economic Data)
