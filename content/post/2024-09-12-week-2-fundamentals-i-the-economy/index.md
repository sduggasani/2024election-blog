---
title: 'Week 2: Fundamentals I, The Economy '
author: Sammy Duggasani
date: '2024-09-12'
slug: []
categories: []
tags: []
---

# **Week 2: Forecasting Fundamentals, the Economy**

**Monday, September 16, 2024**\
**49 Days until Presidential Election**

*Welcome back and thanks for following along my forecast of the 2024 US Presidential Election. Since my last post, Vice President Harris and President Trump faced off in a debate moderated by ABC's Linsey Davis and David Muir. Both candidates were asked about abortion, immigration, foreign policy, and the economy. Only one question was directly asked about the economy, aimed at VP Harris: When it comes to the economy, do you believe Americans are better off than they were four years ago? The focus of this week's post is to build and evaluate models that attempt to illustrate the relationship between incumbent success and measures of the economy.*

## **A Quick Note on Methodology**

I deviate from class-provided data by using *incumbent vote margin* as the outcome variable instead of incumbent two-party-adjusted vote share. There are two main reasons for this. The first is that two-party-adjusted vote metrics do not account for votes for third-party candidates, overlooking potentially significant voter dissatisfaction with the incumbent and/or main challenger candidate. At the same time, the vote margin metric is resistant to the shocks that a potentially "successful" third-party candidate might have on vote share. The second is that vote margin provides us with more insight into the swing between the main candidate: how far ahead was the winner to the runner-up and how close was the election are questions for which the vote margin metric can provide insight.

I source relevant metrics of the economy from a lively discussion between Geoffrey Skelley and Mary Radcliffe on the FiveThirtyEight Politics Podcast Episode "Presidential Debates Do Matter". I highly recommend listening to the episode [here](https://www.youtube.com/watch?v=PkjfKF0frvs&t=1080s). Interestingly, Skelley notes that American voters tend to look to national metrics of the economy in deciding who to vote for more than personal metrics, a phenomenon known as sociotropic voting. I believe there is some truth to this, especially in the ways that changes in national economic performance can trickle down to affect personal finances. Radcliffe and Skelley put together four broad economic phemeona voters internalize as they vote:

-   inflation

-   unemployment

-   personal finances

-   stock market performance

Part of my contribution this week is interpreting these phenomena into specific metrics. I rely on the Consumer Price Index as a measure of inflation, the unemployment rate as a measure of unemployment, quarterly growth in Real Disposable Personal Income as a measure of personal finances, and percent change between SP500 Open and Close reports as a measure of stock market performance. Radcliffe argues that before COVID the price of goods and services and unemployment/jobs were the most salient economic issues to voters. Since shutdowns, though, unemployment has become a much bigger concern for voters.


``` r
#' @title GOV 1347: Week 2 (Economics) Laboratory Session
#' @author Sammy Duggasani
#' @date September 10, 2024

####----------------------------------------------------------#
#### Preamble
####----------------------------------------------------------#

# Load libraries.
## install via `install.packages("name")`
library(car)
```

```
## Loading required package: carData
```

``` r
library(tidyverse)
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2
## ──
```

```
## ✔ ggplot2 3.4.0      ✔ purrr   0.3.5 
## ✔ tibble  3.1.8      ✔ dplyr   1.0.10
## ✔ tidyr   1.2.1      ✔ stringr 1.5.1 
## ✔ readr   2.1.3      ✔ forcats 0.5.2 
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
## ✖ dplyr::recode() masks car::recode()
## ✖ purrr::some()   masks car::some()
```

``` r
library(ggplot2)
library(ggrepel)
library(dplyr)

## set working directory here
setwd("/Users/sammy/Documents/Harvard/Senior Year/2024election-blog/content/post/2024-09-12-week-2-fundamentals-i-the-economy")
# custom ggplot theme
my_prettier_theme <- function() {
  theme(
    # no border
    panel.border = element_blank(),
    # background
    panel.background = element_rect(fill = "snow2"),
    # text
    plot.title = element_text(size = 15, hjust = .5, face = "bold", family = "sans"),
    plot.subtitle = element_text(size = 13, hjust = .5, family = "sans"),
    plot.title.position = "panel",
    axis.text.x = element_text(size = 8, angle = 45, hjust = .5, family = "sans"),
    axis.text.y = element_text(size = 8, family = "sans"),
    axis.title.x = element_text(family = "sans"),
    axis.title.y = element_text(angle = 90, family = "sans"),
    axis.ticks = element_line(colour = "black"),
    axis.line = element_line(colour = "grey"),
    # legend 
    legend.position = "right",
    legend.title = element_text(size = 12, family = "sans"),
    legend.text = element_text(size = 10, family = "sans"),
    # # aspect ratio
    # aspect.ratio = .8
  )
}
```


``` r
####----------------------------------------------------------#
#### Read, merge, and process data.
####----------------------------------------------------------#

# Load popular vote data. 
d_popvote <- read_csv("popvote_1948-2020.csv")
```

```
## Rows: 38 Columns: 9
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (2): party, candidate
## dbl (3): year, pv, pv2p
## lgl (4): winner, incumbent, incumbent_party, prev_admin
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

``` r
# Load economic data from FRED: https://fred.stlouisfed.org. 
# Variables, units, & ranges: 
# GDP, billions $, 1947-2024
# GDP_growth_quarterly, %
# RDPI, $, 1959-2024
# RDPI_growth_quarterly, %
# CPI, $ index, 1947-2024
# unemployment, %, 1948-2024
# sp500_, $, 1927-2024 
d_fred <- read_csv("fred_econ.csv")
```

```
## Rows: 387 Columns: 14
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## dbl (14): year, quarter, GDP, GDP_growth_quarterly, RDPI, RDPI_growth_quarte...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

``` r
# Load economic data from the BEA: https://apps.bea.gov/iTable/?reqid=19&step=2&isuri=1&categories=survey#eyJhcHBpZCI6MTksInN0ZXBzIjpbMSwyLDMsM10sImRhdGEiOltbImNhdGVnb3JpZXMiLCJTdXJ2ZXkiXSxbIk5JUEFfVGFibGVfTGlzdCIsIjI2NCJdLFsiRmlyc3RfWWVhciIsIjE5NDciXSxbIkxhc3RfWWVhciIsIjIwMjQiXSxbIlNjYWxlIiwiMCJdLFsiU2VyaWVzIiwiUSJdXX0=.
# GDP, 1947-2024 (all)
# GNP
# RDPI
# Personal consumption expenditures
# Goods
# Durable goods
# Nondurable goods
# Services 
# Population (midperiod, thousands)
d_bea <- read_csv("bea_econ.csv") |> 
  rename(year = "Year",
         quarter = "Quarter", 
         gdp = "Gross domestic product", 
         gnp = "Gross national product", 
         dpi = "Disposable personal income", 
         consumption = "Personal consumption expenditures", 
         goods = "Goods", 
         durables = "Durable goods", 
         nondurables = "Nondurable goods", 
         services = "Services", 
         pop = "Population (midperiod, thousands)")
```

```
## Rows: 310 Columns: 11
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (1): Quarter
## dbl (10): Year, Gross domestic product, Gross national product, Disposable p...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

``` r
# Filter and merge data. 
d_inc_econ <- d_popvote |> 
  filter(incumbent_party == TRUE) |> 
  select(year, pv, pv2p, winner) |> 
  left_join(d_fred |> filter(quarter == 2)) |> 
  left_join(d_bea |> filter(quarter == "Q2") |> select(year, dpi))
```

```
## Joining, by = "year"
## Joining, by = "year"
```

``` r
# N.B. two different sources of data to use, FRED & BEA. 
# We are using second-quarter data since that is the latest 2024 release. 
# Feel free to experiment with different data/combinations!
```








``` r
# Try using two-party vote margin instead of two-party popular vote share; why: accounts for and more resistant to third-party presence
d_popvote_2 <- read_csv("popvote_1948-2020.csv")
```

```
## Rows: 38 Columns: 9
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (2): party, candidate
## dbl (3): year, pv, pv2p
## lgl (4): winner, incumbent, incumbent_party, prev_admin
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

``` r
d_popvote_2$incumbent_party_name <- ifelse(d_popvote_2$incumbent_party == TRUE, d_popvote_2$party, NA)


d_popvote_wide_2 <- d_popvote_2 |>
  select(year, party, winner, pv, pv2p, incumbent_party_name) |>
  pivot_wider(names_from = party, values_from = c(winner, pv, pv2p, incumbent_party_name))

d_popvote_wide_2 <- d_popvote_wide_2 |>
  mutate(winner = ifelse(winner_democrat == TRUE, "D", "R"),
         incumbent_party_name = ifelse(incumbent_party_name_democrat == "democrat", "D", "R"),
         incumbent_party = replace_na(incumbent_party_name, "R"),
         pv_winner = ifelse(pv_democrat > pv_republican, "D", "R"),
         pv2p = ifelse(incumbent_party == "D", pv2p_democrat, pv2p_republican)) |>
  select(year, winner, incumbent_party, pv_winner, pv_democrat, pv_republican, pv2p_democrat, pv2p_republican, pv2p)
# Adding a variable to give more information about the elections where the popular vote winner was not the electoral college winner, coded as double_win 
d_popvote_wide_2 <- d_popvote_wide_2 |>
  mutate(double_win = ifelse(winner == pv_winner, TRUE, FALSE))

# Add incumbent vote margin variable
d_popvote_wide_2 <- d_popvote_wide_2 |>
  mutate(incumb_vote_margin = ifelse(incumbent_party == "D", pv_democrat - pv_republican, pv_republican-pv_democrat))

# Join with econ info
elec_econ_comb <- d_popvote_wide_2 |>
  left_join(d_fred |> filter(quarter == 2)) |> 
  left_join(d_bea |> filter(quarter == "Q2") |> select(year, dpi))
```

```
## Joining, by = "year"
## Joining, by = "year"
```

## GDP Growth and Vote Margin

*Let's first look at a broad measure of economic performance and evaluate it against incumbent vote margin:*


```
## [1] 0.4334559
```

```
## [1] 0.5632865
```

```
## 
## Call:
## lm(formula = incumb_vote_margin ~ GDP_growth_quarterly, data = elec_econ_comb)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -13.486  -6.655  -1.613   5.163  17.675 
## 
## Coefficients:
##                      Estimate Std. Error t value Pr(>|t|)  
## (Intercept)            2.5596     2.2198   1.153   0.2648  
## GDP_growth_quarterly   0.5330     0.2688   1.983   0.0637 .
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 9.413 on 17 degrees of freedom
## Multiple R-squared:  0.1879,	Adjusted R-squared:  0.1401 
## F-statistic: 3.933 on 1 and 17 DF,  p-value: 0.06374
```

```
## 
## Call:
## lm(formula = incumb_vote_margin ~ GDP_growth_quarterly, data = elec_econ_comb_2)
## 
## Residuals:
##      Min       1Q   Median       3Q      Max 
## -10.9883  -8.1760   0.4772   3.6120  17.3829 
## 
## Coefficients:
##                      Estimate Std. Error t value Pr(>|t|)  
## (Intercept)           -1.0360     2.7711  -0.374   0.7134  
## GDP_growth_quarterly   1.4165     0.5195   2.727   0.0149 *
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 8.732 on 16 degrees of freedom
## Multiple R-squared:  0.3173,	Adjusted R-squared:  0.2746 
## F-statistic: 7.436 on 1 and 16 DF,  p-value: 0.01493
```

```
## Warning: The following aesthetics were dropped during statistical transformation: label
## ℹ This can happen when ggplot fails to infer the correct grouping structure in
##   the data.
## ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
##   variable into a factor?
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-6-1.png" width="672" />

```
## Warning: The following aesthetics were dropped during statistical transformation: label
## ℹ This can happen when ggplot fails to infer the correct grouping structure in
##   the data.
## ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
##   variable into a factor?
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-6-2.png" width="672" />
Here, I run a linear regression on the relationship between between Quarterly GDP Growth and Incumbent Vote Margin, mapping actual election results from 1948 to 2020 onto the plot as well. We observe a pretty strong positive relationship between GDP growth and incumbent vote margin, suggesting that the better the output of the national economy, the better an incumbent party's performance in the upcoming presidential election. You might notice that I have two plots: one with 2020 as a data point and one without. This is because across a number of metrics 2020 is a distant outlier, which often skews models in a ways that confuses any actual evaluation of a relationship between economy and election performance. I keep both plots to illustrate this discrepancy and to note which metrics 2020 data falls into a predicted pattern for and which it does not. 

``` r
# EVALUATING VOTE MARGIN AND GDP GROWTH MODEL

# Evaluate the in-sample fit of your preferred model.
# R-squared method
# With 2020
print(paste("With 2020 R-Squared: ", summary(reg_gdp_margin)$r.squared))
```

```
## [1] "With 2020 R-Squared:  0.187884044842374"
```

``` r
# Without 2020
print(paste("Without 2020 R-Squared: ", summary(reg_gdp_margin_2)$r.squared))
```

```
## [1] "Without 2020 R-Squared:  0.317291723250674"
```

``` r
# In-sample error, plotting residuals
# With 2020
plot(elec_econ_comb$year, elec_econ_comb$incumb_vote_margin, type = "l",
     main ="True Y (Line), Predicted Y (Dot) for Each Year")
points(elec_econ_comb$year, predict(reg_gdp_margin, elec_econ_comb))
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-1.png" width="672" />

``` r
# Without 2020
plot(elec_econ_comb_2$year, elec_econ_comb_2$incumb_vote_margin, type = "l",
     main ="True Y (Line), Predicted Y (Dot) for Each Year")
points(elec_econ_comb_2$year, predict(reg_gdp_margin_2, elec_econ_comb_2))
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-2.png" width="672" />

``` r
# Mean Squared Error
mse_2020 <- mean((reg_gdp_margin$model$incumb_vote_margin - reg_gdp_margin$fitted.values)^2)
mse_no2020 <- mean((reg_gdp_margin_2$model$incumb_vote_margin - reg_gdp_margin_2$fitted.values)^2)
print(paste("With 2020 Mean Squared Error: ", mse_2020))
```

```
## [1] "With 2020 Mean Squared Error:  79.2859405902988"
```

``` r
print(paste("Without 2020 Mean Squared Error: ", mse_no2020))
```

```
## [1] "Without 2020 Mean Squared Error:  67.7703432164646"
```

``` r
# # Model Testing: Leave-One-Out
# (out_samp_pred <- predict(reg_gdp_margin_2, elec_econ_comb_2[elec_econ_comb_2$year == 2020,]))
# (out_samp_truth <- elec_econ_comb |> filter(year == 2020) |> select(incumb_vote_margin))
# print(paste("Leave-One-Out: ", (out_samp_pred - out_samp_truth))) # Dangers of fundamentals-only model!
# # https://www.nytimes.com/2020/07/30/business/economy/q2-gdp-coronavirus-economy.html

# # Model Testing: Cross-Validation (One Run)
# years_out_samp <- sample(elec_econ_comb_2$year, 9) 
# mod <- lm(incumb_vote_margin ~ GDP_growth_quarterly, 
#           elec_econ_comb_2[!(elec_econ_comb_2$year %in% years_out_samp),])
# out_samp_pred <- predict(mod, elec_econ_comb_2[elec_econ_comb_2$year %in% years_out_samp,])
# out_samp_truth <- elec_econ_comb_2$incumb_vote_margin[elec_econ_comb_2$year %in% years_out_samp]
# mean(out_samp_pred - out_samp_truth)

# Model Testing: Cross-Validation (1000 Runs)
out_samp_errors <- sapply(1:1000, function(i) {
  years_out_samp <- sample(elec_econ_comb_2$year, 9) 
  mod <- lm(incumb_vote_margin ~ GDP_growth_quarterly, 
          elec_econ_comb_2[!(elec_econ_comb_2$year %in% years_out_samp),])
  out_samp_pred <- predict(mod, elec_econ_comb_2[elec_econ_comb_2$year %in% years_out_samp,])
  out_samp_truth <- elec_econ_comb_2$incumb_vote_margin[elec_econ_comb_2$year %in% years_out_samp]
  mean(out_samp_pred - out_samp_truth)
})
# mean(out_samp_errors)
print(paste("Cross-Validation Mean Absolute Value Error (Without 2020): ", mean(abs(out_samp_errors))))
```

```
## [1] "Cross-Validation Mean Absolute Value Error (Without 2020):  3.42560959973424"
```
Above are some in-sample and out-of-sample ways to evaluate the strength of GDP Growth model. Across the board, the model performs pretty poorly, as we see very low R-Squared values, high Mean Squared Errors and Cross-Validation Mean Absolute Value Errors with vote margin percentages large enough to sway a close election. The GDP model that leaves out 2020 generally fares better, but it is still not great.  

``` r
####----------------------------------------------------------#
#### Predicting 2024 results using simple GDP and vote margin model.
####----------------------------------------------------------#
# Sequester 2024 data.
GDP_new <- d_fred |> 
  filter(year == 2024 & quarter == 2) |> 
  select(GDP_growth_quarterly)

# Predict.
print(paste("2024 GDP-Predicted Incumbent Vote Margin:", predict(reg_gdp_margin, GDP_new)))
```

```
## [1] "2024 GDP-Predicted Incumbent Vote Margin: 4.15855909921272"
```

``` r
print(paste("2024 GDP-Predicted Incumbent Vote Margin (Excluding 2020 from Model):", predict(reg_gdp_margin_2, GDP_new)))
```

```
## [1] "2024 GDP-Predicted Incumbent Vote Margin (Excluding 2020 from Model): 3.21368743265838"
```
Even still, we can predict how the incumbent party will perform given GDP growth as the input. Across models that involve 2020 and exclude it, it seems that Harris will have a fairly large lead in national popular vote share against Trump. We will tally these outcomes, although flawed in terms of strength of model, as we go along.

**Harris +1**

## CPI and Vote Margin


``` r
####----------------------------------------------------------#
#### Understanding the relationship between economy and vote margin. 
####----------------------------------------------------------#

# Create scatterplot to visualize relationship between CPI and 
# incumbent vote margin 
scatterplot_cpi_margin <- elec_econ_comb |> 
  ggplot(aes(x = CPI, y = incumb_vote_margin, label = year)) + 
  geom_text() + 
  labs(x = "CPI", 
       y = "Incumbent Party's National Popular Vote Margin") + 
  theme_bw()

scatterplot_cpi_margin_2 <- elec_econ_comb_2 |> 
  ggplot(aes(x = CPI, y = incumb_vote_margin, label = year)) + 
  geom_text() + 
  labs(x = "CPI", 
       y = "Incumbent Party's National Popular Vote Margin") + 
  my_prettier_theme()

# Compute correlations between Q2 GDP growth and incumbent vote 2-party vote share.
cor(elec_econ_comb$CPI, 
    elec_econ_comb$incumb_vote_margin)
```

```
## [1] -0.2831376
```

``` r
cor(elec_econ_comb_2$CPI, 
    elec_econ_comb_2$incumb_vote_margin)
```

```
## [1] -0.2280565
```

``` r
# Fit bivariate OLS. 
reg_cpi_margin <- lm(incumb_vote_margin ~ CPI, 
               data = elec_econ_comb)
reg_cpi_margin |> summary() 
```

```
## 
## Call:
## lm(formula = incumb_vote_margin ~ CPI, data = elec_econ_comb)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -17.113  -7.251  -1.099   5.314  17.070 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)  
## (Intercept)  7.52926    3.97750   1.893   0.0755 .
## CPI         -0.03461    0.02843  -1.217   0.2402  
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 10.02 on 17 degrees of freedom
## Multiple R-squared:  0.08017,	Adjusted R-squared:  0.02606 
## F-statistic: 1.482 on 1 and 17 DF,  p-value: 0.2402
```

``` r
reg_cpi_margin_2 <- lm(incumb_vote_margin ~ CPI, 
                 data = elec_econ_comb_2)
reg_cpi_margin_2 |> summary()
```

```
## 
## Call:
## lm(formula = incumb_vote_margin ~ CPI, data = elec_econ_comb_2)
## 
## Residuals:
##      Min       1Q   Median       3Q      Max 
## -16.9232  -7.5255  -0.3135   5.5328  17.1912 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)
## (Intercept)  7.21922    4.18451   1.725    0.104
## CPI         -0.03006    0.03209  -0.937    0.363
## 
## Residual standard error: 10.29 on 16 degrees of freedom
## Multiple R-squared:  0.05201,	Adjusted R-squared:  -0.00724 
## F-statistic: 0.8778 on 1 and 16 DF,  p-value: 0.3627
```

``` r
# Can add bivariate regression lines to our scatterplots. 
regplot_cpi_margin <- elec_econ_comb |> 
  ggplot(aes(x = CPI, y = incumb_vote_margin, label = year)) + 
  geom_smooth(method = "lm", formula = y ~ x) +
  labs(x = "CPI", 
       y = "Incumbent Party's National Popular Vote Margin", 
       title = "Relating CPI and Incumbent Vote Margin",
       subtitle = "Y = 7.52926 + (-0.03461) * X") + 
  geom_text_repel() +
  my_prettier_theme()
regplot_cpi_margin
```

```
## Warning: The following aesthetics were dropped during statistical transformation: label
## ℹ This can happen when ggplot fails to infer the correct grouping structure in
##   the data.
## ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
##   variable into a factor?
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-9-1.png" width="672" />

``` r
regplot_cpi_margin_2 <- elec_econ_comb_2 |> 
  ggplot(aes(x = CPI, y = incumb_vote_margin, label = year)) + 
  geom_smooth(method = "lm", formula = y ~ x) +
  labs(x = "CPI", 
       y = "Incumbent Party's National Popular Vote Margin", 
       title = "Relating CPI and Incumbent Vote Margin",
       subtitle = "Y = 7.21922 + (-0.03006) * X",
       caption = "Excluding 2020 data") + 
  geom_text_repel() +
  my_prettier_theme()
regplot_cpi_margin_2
```

```
## Warning: The following aesthetics were dropped during statistical transformation: label
## ℹ This can happen when ggplot fails to infer the correct grouping structure in
##   the data.
## ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
##   variable into a factor?
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-9-2.png" width="672" />
Above, I run a linear regression on the relationship between between Consumer Price Index and Incumbent Vote Margin. This is a critical measure because voters are exposed to sticker shock effects as a result of inflation and can vote accordingly. It might be a national measure, but individual voters are directly exposed to it. According to the model, there is a pretty strong negative relationship between CPI and incumbent vote margin, suggesting that the higher that consumer prices are, the worse an incumbent party's performance in the upcoming presidential election. Here, it seems that 2020 actually does not distort the model's relationship of the two variables. 


``` r
# EVALUATING VOTE MARGIN AND CPI MODEL

# Evaluate the in-sample fit of your preferred model.
# R-squared method
# With 2020
print(paste("With 2020 R-Squared: ", summary(reg_cpi_margin)$r.squared))
```

```
## [1] "With 2020 R-Squared:  0.0801668996456767"
```

``` r
# Without 2020
print(paste("Without 2020 R-Squared: ", summary(reg_cpi_margin_2)$r.squared))
```

```
## [1] "Without 2020 R-Squared:  0.0520097549971837"
```

``` r
# In-sample error, plotting residuals
# With 2020
plot(elec_econ_comb$year, elec_econ_comb$incumb_vote_margin, type = "l",
     main ="True Y (Line), Predicted Y (Dot) for Each Year")
points(elec_econ_comb$year, predict(reg_cpi_margin, elec_econ_comb))
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-10-1.png" width="672" />

``` r
# Without 2020
plot(elec_econ_comb_2$year, elec_econ_comb_2$incumb_vote_margin, type = "l",
     main ="True Y (Line), Predicted Y (Dot) for Each Year")
points(elec_econ_comb_2$year, predict(reg_cpi_margin_2, elec_econ_comb_2))
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-10-2.png" width="672" />

``` r
# Mean Squared Error
mse_2020 <- mean((reg_cpi_margin$model$incumb_vote_margin - reg_cpi_margin$fitted.values)^2)
mse_no2020 <- mean((reg_cpi_margin_2$model$incumb_vote_margin - reg_cpi_margin_2$fitted.values)^2)
print(paste("With 2020 Mean Squared Error: ", mse_2020))
```

```
## [1] "With 2020 Mean Squared Error:  89.8022407816482"
```

``` r
print(paste("Without 2020 Mean Squared Error: ", mse_no2020))
```

```
## [1] "Without 2020 Mean Squared Error:  94.1040653199678"
```

``` r
# # Model Testing: Leave-One-Out
# (out_samp_pred <- predict(reg_cpi_margin_2, elec_econ_comb_2[elec_econ_comb_2$year == 2020,]))
# (out_samp_truth <- elec_econ_comb_2 |> filter(year == 2020) |> select(incumb_vote_margin))
# print(paste("Leave-One-Out: ", (out_samp_pred - out_samp_truth))) # Dangers of fundamentals-only model!
# # https://www.nytimes.com/2020/07/30/business/economy/q2-gdp-coronavirus-economy.html

# # Model Testing: Cross-Validation (One Run)
# years_out_samp <- sample(elec_econ_comb_2$year, 9) 
# mod <- lm(incumb_vote_margin ~ GDP_growth_quarterly, 
#           elec_econ_comb_2[!(elec_econ_comb_2$year %in% years_out_samp),])
# out_samp_pred <- predict(mod, elec_econ_comb_2[elec_econ_comb_2$year %in% years_out_samp,])
# out_samp_truth <- elec_econ_comb_2$incumb_vote_margin[elec_econ_comb_2$year %in% years_out_samp]
# mean(out_samp_pred - out_samp_truth)

# Model Testing: Cross-Validation (1000 Runs)
out_samp_errors <- sapply(1:1000, function(i) {
  years_out_samp <- sample(elec_econ_comb_2$year, 9) 
  mod <- lm(incumb_vote_margin ~ CPI, 
          elec_econ_comb_2[!(elec_econ_comb_2$year %in% years_out_samp),])
  out_samp_pred <- predict(mod, elec_econ_comb_2[elec_econ_comb_2$year %in% years_out_samp,])
  out_samp_truth <- elec_econ_comb_2$incumb_vote_margin[elec_econ_comb_2$year %in% years_out_samp]
  mean(out_samp_pred - out_samp_truth)
})
# mean(out_samp_errors)
print(paste("Cross-Validation Mean Absolute Value Error (Without 2020): ", mean(abs(out_samp_errors))))
```

```
## [1] "Cross-Validation Mean Absolute Value Error (Without 2020):  4.30330631116584"
```

The CPI model fares even worse than the GDP model with abysmal R-Squared values, high Mean Squared Errors, and a large Cross-Validation Mean Absolute Value Error.


``` r
####----------------------------------------------------------#
#### Predicting 2024 results using simple CPI and vote margin model.
####----------------------------------------------------------#
# Sequester 2024 data.
CPI_new <- d_fred |> 
  filter(year == 2024 & quarter == 2) |> 
  select(CPI)

# Predict.
print(paste("2024 CPI-Predicted Incumbent Vote Margin:", predict(reg_cpi_margin, CPI_new)))
```

```
## [1] "2024 CPI-Predicted Incumbent Vote Margin: -3.30839041076806"
```

``` r
print(paste("2024 CPI-Predicted Incumbent Vote Margin (Excluding 2020 from Model):", predict(reg_cpi_margin_2, CPI_new)))
```

```
## [1] "2024 CPI-Predicted Incumbent Vote Margin (Excluding 2020 from Model): -2.19490995507331"
```

Building our linear regression model on solely the CPI, we see that Harris trails Trump by 3.3% share of national popular vote with 2020 data and 2.2% excluding it. This makes sense as voters have consistently aired their grievances about inflation through this campaign season.

**Trump +1**

## RDPI Growth and Vote Margin


``` r
####----------------------------------------------------------#
#### Understanding the relationship between economy and vote margin. 
####----------------------------------------------------------#

# Create scatterplot to visualize relationship between RDPI Growth and 
# incumbent vote margin 
scatterplot_rdpi_margin <- elec_econ_comb |> 
  ggplot(aes(x = RDPI_growth_quarterly, y = incumb_vote_margin, label = year)) + 
  geom_text() + 
  labs(x = "RDPI Quarterly Growth (%)", 
       y = "Incumbent Party's National Popular Vote Margin") + 
  theme_bw()

scatterplot_rdpi_margin_2 <- elec_econ_comb_2 |> 
  ggplot(aes(x = RDPI_growth_quarterly, y = incumb_vote_margin, label = year)) + 
  geom_text() + 
  labs(x = "RDPI Quarterly Growth (%)", 
       y = "Incumbent Party's National Popular Vote Margin") + 
  my_prettier_theme()

# Compute correlations between Q2 GDP growth and incumbent vote 2-party vote share.
cor(elec_econ_comb$RDPI_growth_quarterly, 
    elec_econ_comb$incumb_vote_margin)
```

```
## [1] -0.0596564
```

``` r
cor(elec_econ_comb_2$RDPI_growth_quarterly, 
    elec_econ_comb_2$incumb_vote_margin)
```

```
## [1] 0.3304367
```

``` r
# Fit bivariate OLS. 
reg_rdpi_margin <- lm(incumb_vote_margin ~ RDPI_growth_quarterly, 
               data = elec_econ_comb)
reg_rdpi_margin |> summary() 
```

```
## 
## Call:
## lm(formula = incumb_vote_margin ~ RDPI_growth_quarterly, data = elec_econ_comb)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -14.175  -5.886  -1.894   4.348  19.426 
## 
## Coefficients:
##                       Estimate Std. Error t value Pr(>|t|)
## (Intercept)             3.9848     2.9067   1.371    0.188
## RDPI_growth_quarterly  -0.0597     0.2423  -0.246    0.808
## 
## Residual standard error: 10.43 on 17 degrees of freedom
## Multiple R-squared:  0.003559,	Adjusted R-squared:  -0.05506 
## F-statistic: 0.06072 on 1 and 17 DF,  p-value: 0.8083
```

``` r
reg_rdpi_margin_2 <- lm(incumb_vote_margin ~ RDPI_growth_quarterly, 
                 data = elec_econ_comb_2)
reg_rdpi_margin_2 |> summary()
```

```
## 
## Call:
## lm(formula = incumb_vote_margin ~ RDPI_growth_quarterly, data = elec_econ_comb_2)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -15.012  -6.463  -1.750   4.939  19.535 
## 
## Coefficients:
##                       Estimate Std. Error t value Pr(>|t|)
## (Intercept)           -0.09853    3.76747  -0.026    0.979
## RDPI_growth_quarterly  0.88662    0.63312   1.400    0.180
## 
## Residual standard error: 9.974 on 16 degrees of freedom
## Multiple R-squared:  0.1092,	Adjusted R-squared:  0.05351 
## F-statistic: 1.961 on 1 and 16 DF,  p-value: 0.1805
```

``` r
# Can add bivariate regression lines to our scatterplots. 
regplot_rdpi_margin <- elec_econ_comb |> 
  ggplot(aes(x = RDPI_growth_quarterly, y = incumb_vote_margin, label = year)) + 
  geom_smooth(method = "lm", formula = y ~ x) +
  labs(x = "RDPI Quarterly Growth (%)", 
       y = "Incumbent Party's National Popular Vote Margin", 
       title = "Relating RDPI Growth and Incumbent Vote Margin",
       subtitle = "Y = 3.9848 + (-0.0597) * X") + 
  geom_text_repel() +
  my_prettier_theme()
regplot_rdpi_margin
```

```
## Warning: The following aesthetics were dropped during statistical transformation: label
## ℹ This can happen when ggplot fails to infer the correct grouping structure in
##   the data.
## ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
##   variable into a factor?
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-12-1.png" width="672" />

``` r
regplot_rdpi_margin_2 <- elec_econ_comb_2 |> 
  ggplot(aes(x = RDPI_growth_quarterly, y = incumb_vote_margin, label = year)) + 
  geom_smooth(method = "lm", formula = y ~ x) +
  labs(x = "RDPI Quarterly Growth (%)", 
       y = "Incumbent Party's National Popular Vote Margin", 
       title = "Relating RDPI Growth and Incumbent Vote Margin",
       subtitle = "Y = -0.09853 + 0.88662 * X",
       caption = "Excluding 2020 data") + 
  geom_text_repel() +
  my_prettier_theme()
regplot_rdpi_margin_2
```

```
## Warning: The following aesthetics were dropped during statistical transformation: label
## ℹ This can happen when ggplot fails to infer the correct grouping structure in
##   the data.
## ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
##   variable into a factor?
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-12-2.png" width="672" />
Now, I run a linear regression on the relationship between between Quarterly Growth in Real Disposable Personal Income and Incumbent Vote Margin. RDPI is my proxy for personal finances and can provide insight into how much voters are actually working with after taxes. According to the model, there is a pretty strong positive relationship between RDPI and incumbent vote margin, suggesting that the greater growth in RDPI, the better an incumbent party's performance in the upcoming presidential election. Here, it seems that 2020 completely distorts the model's relationship of the two variables, so it is probably best to leave it out. 


``` r
# EVALUATING VOTE MARGIN AND RDPI MODEL

# Evaluate the in-sample fit of your preferred model.
# R-squared method
# With 2020
print(paste("With 2020 R-Squared: ", summary(reg_rdpi_margin)$r.squared))
```

```
## [1] "With 2020 R-Squared:  0.00355888626006062"
```

``` r
# Without 2020
print(paste("Without 2020 R-Squared: ", summary(reg_rdpi_margin_2)$r.squared))
```

```
## [1] "Without 2020 R-Squared:  0.109188411395232"
```

``` r
# In-sample error, plotting residuals
# With 2020
plot(elec_econ_comb$year, elec_econ_comb$incumb_vote_margin, type = "l",
     main ="True Y (Line), Predicted Y (Dot) for Each Year")
points(elec_econ_comb$year, predict(reg_rdpi_margin, elec_econ_comb))
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-13-1.png" width="672" />

``` r
# Without 2020
plot(elec_econ_comb_2$year, elec_econ_comb_2$incumb_vote_margin, type = "l",
     main ="True Y (Line), Predicted Y (Dot) for Each Year")
points(elec_econ_comb_2$year, predict(reg_rdpi_margin_2, elec_econ_comb_2))
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-13-2.png" width="672" />

``` r
# Mean Squared Error
mse_2020 <- mean((reg_rdpi_margin$model$incumb_vote_margin - reg_rdpi_margin$fitted.values)^2)
mse_no2020 <- mean((reg_rdpi_margin_2$model$incumb_vote_margin - reg_rdpi_margin_2$fitted.values)^2)
print(paste("With 2020 Mean Squared Error: ", mse_2020))
```

```
## [1] "With 2020 Mean Squared Error:  97.2813924464543"
```

``` r
print(paste("Without 2020 Mean Squared Error: ", mse_no2020))
```

```
## [1] "Without 2020 Mean Squared Error:  88.4281166011348"
```

``` r
# # Model Testing: Leave-One-Out
# (out_samp_pred <- predict(reg_rdpi_margin_2, elec_econ_comb_2[elec_econ_comb_2$year == 2020,]))
# (out_samp_truth <- elec_econ_comb_2 |> filter(year == 2020) |> select(incumb_vote_margin))
# print(paste("Leave-One-Out: ", (out_samp_pred - out_samp_truth))) # Dangers of fundamentals-only model!
# # https://www.nytimes.com/2020/07/30/business/economy/q2-gdp-coronavirus-economy.html

# # Model Testing: Cross-Validation (One Run)
# years_out_samp <- sample(elec_econ_comb_2$year, 9) 
# mod <- lm(incumb_vote_margin ~ GDP_growth_quarterly, 
#           elec_econ_comb_2[!(elec_econ_comb_2$year %in% years_out_samp),])
# out_samp_pred <- predict(mod, elec_econ_comb_2[elec_econ_comb_2$year %in% years_out_samp,])
# out_samp_truth <- elec_econ_comb_2$incumb_vote_margin[elec_econ_comb_2$year %in% years_out_samp]
# mean(out_samp_pred - out_samp_truth)

# Model Testing: Cross-Validation (1000 Runs)
out_samp_errors <- sapply(1:1000, function(i) {
  years_out_samp <- sample(elec_econ_comb_2$year, 9) 
  mod <- lm(incumb_vote_margin ~ RDPI_growth_quarterly, 
          elec_econ_comb_2[!(elec_econ_comb_2$year %in% years_out_samp),])
  out_samp_pred <- predict(mod, elec_econ_comb_2[elec_econ_comb_2$year %in% years_out_samp,])
  out_samp_truth <- elec_econ_comb_2$incumb_vote_margin[elec_econ_comb_2$year %in% years_out_samp]
  mean(out_samp_pred - out_samp_truth)
})
# mean(out_samp_errors)
print(paste("Cross-Validation Mean Absolute Value Error (Without 2020): ", mean(abs(out_samp_errors))))
```

```
## [1] "Cross-Validation Mean Absolute Value Error (Without 2020):  4.1182564160077"
```
Again, the RDPI model performs pretty poorly with in-sample and out-of-sample tests. It yields low R-Squared values even when I leave out 2020 data. The Mean Squared Error is high and so is the Cross-Validation Mean Absolute Value Error. 


``` r
####----------------------------------------------------------#
#### Predicting 2024 results using simple RDPI Growth and vote margin model.
####----------------------------------------------------------#
# Sequester 2024 data.
RDPI_new <- d_fred |> 
  filter(year == 2024 & quarter == 2) |> 
  select(RDPI_growth_quarterly)

# Predict.
print(paste("2024 RDPI Growth-Predicted Incumbent Vote Margin:", predict(reg_rdpi_margin, RDPI_new)))
```

```
## [1] "2024 RDPI Growth-Predicted Incumbent Vote Margin: 3.9250814230794"
```

``` r
print(paste("2024 RDPI Growth-Predicted Incumbent Vote Margin (Excluding 2020 from Model):", predict(reg_rdpi_margin_2, RDPI_new)))
```

```
## [1] "2024 RDPI Growth-Predicted Incumbent Vote Margin (Excluding 2020 from Model): 0.788092792500218"
```
However, if we use this model to forecast the upcoming election, it appears that Harris will win. The model that involves 2020 data I determined was extremely flawed for distorting the input-outcome relationship. When we exclude 2020 data, it appears that Harris only wins the national popular vote share by less than a percentage, signaling a close race (if Quarterly RDPI Growth is all that mattered to voters).

**Harris +1**

## Unemployment and Vote Margin


``` r
####----------------------------------------------------------#
#### Understanding the relationship between economy and vote margin. 
####----------------------------------------------------------#

# Create scatterplot to visualize relationship between Unemployment and 
# incumbent vote margin 
scatterplot_unemp_margin <- elec_econ_comb |> 
  ggplot(aes(x = unemployment, y = incumb_vote_margin, label = year)) + 
  geom_text() + 
  labs(x = "Unemployment Rate (%)", 
       y = "Incumbent Party's National Popular Vote Margin") + 
  theme_bw()

scatterplot_unemp_margin_2 <- elec_econ_comb_2 |> 
  ggplot(aes(x = unemployment, y = incumb_vote_margin, label = year)) + 
  geom_text() + 
  labs(x = "Unemployment Rate (%)", 
       y = "Incumbent Party's National Popular Vote Margin") + 
  my_prettier_theme()

# Compute correlations between Q2 Unemployment and incumbent vote 2-party vote share.
cor(elec_econ_comb$unemployment, 
    elec_econ_comb$incumb_vote_margin)
```

```
## [1] -0.1287775
```

``` r
cor(elec_econ_comb_2$unemployment, 
    elec_econ_comb_2$incumb_vote_margin)
```

```
## [1] 0.02293066
```

``` r
# Fit bivariate OLS. 
reg_unemp_margin <- lm(incumb_vote_margin ~ unemployment, 
               data = elec_econ_comb)
reg_unemp_margin |> summary() 
```

```
## 
## Call:
## lm(formula = incumb_vote_margin ~ unemployment, data = elec_econ_comb)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -15.764  -5.236  -2.002   4.256  19.458 
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)
## (Intercept)    6.9590     6.7471   1.031    0.317
## unemployment  -0.5714     1.0671  -0.535    0.599
## 
## Residual standard error: 10.36 on 17 degrees of freedom
## Multiple R-squared:  0.01658,	Adjusted R-squared:  -0.04126 
## F-statistic: 0.2867 on 1 and 17 DF,  p-value: 0.5993
```

``` r
reg_unemp_margin_2 <- lm(incumb_vote_margin ~ unemployment, 
                 data = elec_econ_comb_2)
reg_unemp_margin_2 |> summary()
```

```
## 
## Call:
## lm(formula = incumb_vote_margin ~ unemployment, data = elec_econ_comb_2)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -14.139  -6.019  -1.664   4.323  19.109 
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)
## (Intercept)    3.1909     9.4185   0.339    0.739
## unemployment   0.1509     1.6443   0.092    0.928
## 
## Residual standard error: 10.56 on 16 degrees of freedom
## Multiple R-squared:  0.0005258,	Adjusted R-squared:  -0.06194 
## F-statistic: 0.008417 on 1 and 16 DF,  p-value: 0.928
```

``` r
# Can add bivariate regression lines to our scatterplots. 
regplot_unemp_margin <- elec_econ_comb |> 
  ggplot(aes(x = unemployment, y = incumb_vote_margin, label = year)) + 
  geom_smooth(method = "lm", formula = y ~ x) +
  labs(x = "Unemployment Rate (%)", 
       y = "Incumbent Party's National Popular Vote Margin", 
       title = "Relating Unemployment Rate and Incumbent Vote Margin",
       subtitle = "Y = 6.9590 + (-0.5714) * X") + 
  geom_text_repel() +
  my_prettier_theme()
regplot_unemp_margin
```

```
## Warning: The following aesthetics were dropped during statistical transformation: label
## ℹ This can happen when ggplot fails to infer the correct grouping structure in
##   the data.
## ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
##   variable into a factor?
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-15-1.png" width="672" />

``` r
regplot_unemp_margin_2 <- elec_econ_comb_2 |> 
  ggplot(aes(x = unemployment, y = incumb_vote_margin, label = year)) + 
  geom_smooth(method = "lm", formula = y ~ x) +
  labs(x = "Unemployment Rate (%)", 
       y = "Incumbent Party's National Popular Vote Margin", 
       title = "Relating Unemployment Rate and Incumbent Vote Margin",
       subtitle = "Y = 3.1909 + 0.1509 * X",
       caption = "Excluding 2020 data") + 
  geom_text_repel() +
  my_prettier_theme()
regplot_unemp_margin_2
```

```
## Warning: The following aesthetics were dropped during statistical transformation: label
## ℹ This can happen when ggplot fails to infer the correct grouping structure in
##   the data.
## ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
##   variable into a factor?
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-15-2.png" width="672" />
Continuing with the economic phenomena Radcliffe and Skelley highlight as important to voters, I run a linear regression on the relationship between between Unemployment and Incumbent Vote Margin. Interestingly, the model suggests that there is no correlation  between unemployment and incumbent vote margin, especially if we look at the one that excludes 2020 data. It makes sense to exclude 2020 here because it forces a relationship that looks like does not exist.


``` r
# EVALUATING VOTE MARGIN AND Unemployment MODEL

# Evaluate the in-sample fit of your preferred model.
# R-squared method
# With 2020
print(paste("With 2020 R-Squared: ", summary(reg_unemp_margin)$r.squared))
```

```
## [1] "With 2020 R-Squared:  0.0165836375771564"
```

``` r
# Without 2020
print(paste("Without 2020 R-Squared: ", summary(reg_unemp_margin_2)$r.squared))
```

```
## [1] "Without 2020 R-Squared:  0.00052581496233859"
```

``` r
# In-sample error, plotting residuals
# With 2020
plot(elec_econ_comb$year, elec_econ_comb$incumb_vote_margin, type = "l",
     main ="True Y (Line), Predicted Y (Dot) for Each Year")
points(elec_econ_comb$year, predict(reg_unemp_margin, elec_econ_comb))
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-16-1.png" width="672" />

``` r
# Without 2020
plot(elec_econ_comb_2$year, elec_econ_comb_2$incumb_vote_margin, type = "l",
     main ="True Y (Line), Predicted Y (Dot) for Each Year")
points(elec_econ_comb_2$year, predict(reg_unemp_margin_2, elec_econ_comb_2))
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-16-2.png" width="672" />

``` r
# Mean Squared Error
mse_2020 <- mean((reg_unemp_margin$model$incumb_vote_margin - reg_unemp_margin$fitted.values)^2)
mse_no2020 <- mean((reg_unemp_margin_2$model$incumb_vote_margin - reg_unemp_margin_2$fitted.values)^2)
print(paste("With 2020 Mean Squared Error: ", mse_2020))
```

```
## [1] "With 2020 Mean Squared Error:  96.0098010529196"
```

``` r
print(paste("Without 2020 Mean Squared Error: ", mse_no2020))
```

```
## [1] "Without 2020 Mean Squared Error:  99.2147171241475"
```

``` r
# # Model Testing: Leave-One-Out
# (out_samp_pred <- predict(reg_unemp_margin_2, elec_econ_comb_2[elec_econ_comb_2$year == 2020,]))
# (out_samp_truth <- elec_econ_comb_2 |> filter(year == 2020) |> select(incumb_vote_margin))
# print(paste("Leave-One-Out: ", (out_samp_pred - out_samp_truth))) # Dangers of fundamentals-only model!
# https://www.nytimes.com/2020/07/30/business/economy/q2-gdp-coronavirus-economy.html

# # Model Testing: Cross-Validation (One Run)
# years_out_samp <- sample(elec_econ_comb_2$year, 9) 
# mod <- lm(incumb_vote_margin ~ GDP_growth_quarterly, 
#           elec_econ_comb_2[!(elec_econ_comb_2$year %in% years_out_samp),])
# out_samp_pred <- predict(mod, elec_econ_comb_2[elec_econ_comb_2$year %in% years_out_samp,])
# out_samp_truth <- elec_econ_comb_2$incumb_vote_margin[elec_econ_comb_2$year %in% years_out_samp]
# mean(out_samp_pred - out_samp_truth)

# Model Testing: Cross-Validation (1000 Runs)
out_samp_errors <- sapply(1:1000, function(i) {
  years_out_samp <- sample(elec_econ_comb_2$year, 9) 
  mod <- lm(incumb_vote_margin ~ unemployment, 
          elec_econ_comb_2[!(elec_econ_comb_2$year %in% years_out_samp),])
  out_samp_pred <- predict(mod, elec_econ_comb_2[elec_econ_comb_2$year %in% years_out_samp,])
  out_samp_truth <- elec_econ_comb_2$incumb_vote_margin[elec_econ_comb_2$year %in% years_out_samp]
  mean(out_samp_pred - out_samp_truth)
})
# mean(out_samp_errors)
print(paste("Cross-Validation Mean Absolute Value Error (Without 2020): ", mean(abs(out_samp_errors))))
```

```
## [1] "Cross-Validation Mean Absolute Value Error (Without 2020):  4.27701705434377"
```
The R-Squared values for the unemployment-predicted model are the lowest we have seen so far. THe Mean Squared Errors are also the highest and the Cross-Validation Mean Absolute Value Error is a large percentage vote margin that could push an election in any direction. 


``` r
####----------------------------------------------------------#
#### Predicting 2024 results using simple GDP and vote margin model.
####----------------------------------------------------------#
# Sequester 2024 data.
unemp_new <- d_fred |> 
  filter(year == 2024 & quarter == 2) |> 
  select(unemployment)

# Predict.
print(paste("2024 Unemployment-Predicted Incumbent Vote Margin:", predict(reg_unemp_margin, unemp_new)))
```

```
## [1] "2024 Unemployment-Predicted Incumbent Vote Margin: 4.67350537665337"
```

``` r
print(paste("2024 Unemployment-Predicted Incumbent Vote Margin (Excluding 2020 from Model):", predict(reg_unemp_margin_2, unemp_new)))
```

```
## [1] "2024 Unemployment-Predicted Incumbent Vote Margin (Excluding 2020 from Model): 3.79434427081865"
```
The model suggests that the incumbent party, Harris and the Democrats, will win the national popular vote share in November—whether we include 2020 data or not. 

**Harris +1**

## Stock Market Performance and Vote Margin


``` r
####----------------------------------------------------------#
#### Understanding the relationship between economy and vote margin. 
####----------------------------------------------------------#

# Create Stock Margin Performance Variable (as percentage change)
elec_econ_comb <- elec_econ_comb |>
  mutate(sp500_perf = (sp500_close-sp500_open)/(sp500_open)*100)
elec_econ_comb_2 <- elec_econ_comb_2 |>
  mutate(sp500_perf = (sp500_close-sp500_open)/(sp500_open)*100)

# Create scatterplot to visualize relationship between Stock Market and 
# incumbent vote margin 
scatterplot_stock_margin <- elec_econ_comb |> 
  ggplot(aes(x = sp500_perf, y = incumb_vote_margin, label = year)) + 
  geom_text() + 
  labs(x = "Stock Market Open-Close Change (%)", 
       y = "Incumbent Party's National Popular Vote Margin") + 
  theme_bw()

scatterplot_stock_margin_2 <- elec_econ_comb_2 |> 
  ggplot(aes(x = sp500_perf, y = incumb_vote_margin, label = year)) + 
  geom_text() + 
  labs(x = "Stock Market Open-Close Change (%)", 
       y = "Incumbent Party's National Popular Vote Margin") + 
  my_prettier_theme()

# Compute correlations between Q2 Unemployment and incumbent vote 2-party vote share.
cor(elec_econ_comb$sp500_perf, 
    elec_econ_comb$incumb_vote_margin)
```

```
## [1] -0.3389181
```

``` r
cor(elec_econ_comb_2$sp500_perf, 
    elec_econ_comb_2$incumb_vote_margin)
```

```
## [1] -0.2969328
```

``` r
# Fit bivariate OLS. 
reg_stock_margin <- lm(incumb_vote_margin ~ sp500_perf, 
               data = elec_econ_comb)
reg_stock_margin |> summary() 
```

```
## 
## Call:
## lm(formula = incumb_vote_margin ~ sp500_perf, data = elec_econ_comb)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -14.388  -6.502  -2.020   5.282  19.102 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)  
## (Intercept)    5.245      2.518   2.083   0.0527 .
## sp500_perf    -1.557      1.048  -1.485   0.1558  
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 9.828 on 17 degrees of freedom
## Multiple R-squared:  0.1149,	Adjusted R-squared:  0.0628 
## F-statistic: 2.206 on 1 and 17 DF,  p-value: 0.1558
```

``` r
reg_stock_margin_2 <- lm(incumb_vote_margin ~ sp500_perf, 
                 data = elec_econ_comb_2)
reg_stock_margin_2 |> summary()
```

```
## 
## Call:
## lm(formula = incumb_vote_margin ~ sp500_perf, data = elec_econ_comb_2)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -14.996  -6.818  -1.964   5.794  19.409 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)  
## (Intercept)    5.398      2.622   2.058   0.0562 .
## sp500_perf    -1.963      1.578  -1.244   0.2315  
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 10.09 on 16 degrees of freedom
## Multiple R-squared:  0.08817,	Adjusted R-squared:  0.03118 
## F-statistic: 1.547 on 1 and 16 DF,  p-value: 0.2315
```

``` r
# Can add bivariate regression lines to our scatterplots. 
regplot_stock_margin <- elec_econ_comb |> 
  ggplot(aes(x = sp500_perf, y = incumb_vote_margin, label = year)) + 
  geom_smooth(method = "lm", formula = y ~ x) +
  labs(x = "Stock Market Open-Close Change (%)", 
       y = "Incumbent Party's National Popular Vote Margin", 
       title = "Relating Stock Market Performance and Incumbent Vote Margin",
       subtitle = "Y = 5.245 + (-1.557) * X") + 
  geom_text_repel() +
  my_prettier_theme()
regplot_stock_margin
```

```
## Warning: The following aesthetics were dropped during statistical transformation: label
## ℹ This can happen when ggplot fails to infer the correct grouping structure in
##   the data.
## ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
##   variable into a factor?
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-18-1.png" width="672" />

``` r
regplot_stock_margin_2 <- elec_econ_comb_2 |> 
  ggplot(aes(x = sp500_perf, y = incumb_vote_margin, label = year)) + 
  geom_smooth(method = "lm", formula = y ~ x) +
  labs(x = "Stock Market Open-Close Change (%)", 
       y = "Incumbent Party's National Popular Vote Margin", 
       title = "Relating Stock Market Performance and Incumbent Vote Margin",
       subtitle = "Y = 5.398 + (-1.963) * X",
       caption = "Excluding 2020 data") + 
  geom_text_repel() +
  my_prettier_theme()
regplot_stock_margin_2
```

```
## Warning: The following aesthetics were dropped during statistical transformation: label
## ℹ This can happen when ggplot fails to infer the correct grouping structure in
##   the data.
## ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
##   variable into a factor?
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-18-2.png" width="672" />

Finally, we look to stock market performance as a metric of economic success that voters find salient. Both 2020-inclusive and 2020-exclusive models suggest a negative relationship between Stock Market Change and Incumbent Vote Margin. This is counter-intuitive because it suggests that greater growth of the SP500 coincides with poorer performance of the incumbent party in an upcoming election. It might be that higher percentage stock market changes actually signal a volatile economy that voters fear; this is speculative though and not an actual attempt to establish causality. 



``` r
# EVALUATING VOTE MARGIN AND Stock MODEL

# Evaluate the in-sample fit of your preferred model.
# R-squared method
# With 2020
print(paste("With 2020 R-Squared: ", summary(reg_stock_margin)$r.squared))
```

```
## [1] "With 2020 R-Squared:  0.114865484041972"
```

``` r
# Without 2020
print(paste("Without 2020 R-Squared: ", summary(reg_stock_margin_2)$r.squared))
```

```
## [1] "Without 2020 R-Squared:  0.0881691133665322"
```

``` r
# In-sample error, plotting residuals
# With 2020
plot(elec_econ_comb$year, elec_econ_comb$incumb_vote_margin, type = "l",
     main ="True Y (Line), Predicted Y (Dot) for Each Year")
points(elec_econ_comb$year, predict(reg_stock_margin, elec_econ_comb))
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-19-1.png" width="672" />

``` r
# Without 2020
plot(elec_econ_comb_2$year, elec_econ_comb_2$incumb_vote_margin, type = "l",
     main ="True Y (Line), Predicted Y (Dot) for Each Year")
points(elec_econ_comb_2$year, predict(reg_stock_margin_2, elec_econ_comb_2))
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-19-2.png" width="672" />

``` r
# Mean Squared Error
mse_2020 <- mean((reg_stock_margin$model$incumb_vote_margin - reg_stock_margin$fitted.values)^2)
mse_no2020 <- mean((reg_stock_margin_2$model$incumb_vote_margin - reg_stock_margin_2$fitted.values)^2)
print(paste("With 2020 Mean Squared Error: ", mse_2020))
```

```
## [1] "With 2020 Mean Squared Error:  86.4146581543887"
```

``` r
print(paste("Without 2020 Mean Squared Error: ", mse_no2020))
```

```
## [1] "Without 2020 Mean Squared Error:  90.5146374330731"
```

``` r
# # Model Testing: Leave-One-Out
# (out_samp_pred <- predict(reg_stock_margin_2, elec_econ_comb_2[elec_econ_comb_2$year == 2020,]))
# (out_samp_truth <- elec_econ_comb_2 |> filter(year == 2020) |> select(incumb_vote_margin))
# print(paste("Leave-One-Out: ", (out_samp_pred - out_samp_truth))) # Dangers of fundamentals-only model!
# https://www.nytimes.com/2020/07/30/business/economy/q2-gdp-coronavirus-economy.html

# # Model Testing: Cross-Validation (One Run)
# years_out_samp <- sample(elec_econ_comb_2$year, 9) 
# mod <- lm(incumb_vote_margin ~ GDP_growth_quarterly, 
#           elec_econ_comb_2[!(elec_econ_comb_2$year %in% years_out_samp),])
# out_samp_pred <- predict(mod, elec_econ_comb_2[elec_econ_comb_2$year %in% years_out_samp,])
# out_samp_truth <- elec_econ_comb_2$incumb_vote_margin[elec_econ_comb_2$year %in% years_out_samp]
# mean(out_samp_pred - out_samp_truth)

# Model Testing: Cross-Validation (1000 Runs)
out_samp_errors <- sapply(1:1000, function(i) {
  years_out_samp <- sample(elec_econ_comb_2$year, 9) 
  mod <- lm(incumb_vote_margin ~ sp500_perf, 
          elec_econ_comb_2[!(elec_econ_comb_2$year %in% years_out_samp),])
  out_samp_pred <- predict(mod, elec_econ_comb_2[elec_econ_comb_2$year %in% years_out_samp,])
  out_samp_truth <- elec_econ_comb_2$incumb_vote_margin[elec_econ_comb_2$year %in% years_out_samp]
  mean(out_samp_pred - out_samp_truth)
})
# mean(out_samp_errors)
print(paste("Cross-Validation Mean Absolute Value Error (Without 2020): ", mean(abs(out_samp_errors))))
```

```
## [1] "Cross-Validation Mean Absolute Value Error (Without 2020):  4.08597249172685"
```

Like the rest, the stock market model performs poorly in measures of in-sample and out-of-sample testing. The R-Squared values are low, the Mean Square Errors are high, and the Cross-Validation Mean Absolute Value is a large percentage value.


``` r
####----------------------------------------------------------#
#### Predicting 2024 results using simple GDP and vote margin model.
####----------------------------------------------------------#
# Sequester 2024 data.
stock_new <- d_fred |> 
  filter(year == 2024 & quarter == 2) |>
  mutate(sp500_perf = (sp500_close-sp500_open)/(sp500_open)*100)|>
  select(sp500_perf)

# Predict.
print(paste("2024 Stock Market-Predicted Incumbent Vote Margin:", predict(reg_stock_margin, stock_new)))
```

```
## [1] "2024 Stock Market-Predicted Incumbent Vote Margin: 3.99855641825043"
```

``` r
print(paste("2024 Stock Market--Predicted Incumbent Vote Margin (Excluding 2020 from Model):", predict(reg_stock_margin_2, stock_new)))
```

```
## [1] "2024 Stock Market--Predicted Incumbent Vote Margin (Excluding 2020 from Model): 3.8267002013802"
```
When we predict incumbent vote margin using this model, we get that Harris will be ahead of Trump by about 4 points with regards to the national popular vote share. 

**Harris +1**

## Conclusion

**Harris: 4**/
**Trump: 1**/
**Prediction: Harris will win the popular vote in November.** 

If we treat each metric of the economy (that I used to run these regressions) as keys, we see that Harris has won four economic keys and Trump has won just one. This deviates from Skelley's suggestion that retrospective voters will disfavor Harris in light of their economic grievances. 

In all honesty, these models are quite bad. I would not put my money on the prediction resultant from them. The best model by in-sample and out-of-sample metrics was the Quarterly-GDP-Growth-Predicted Model, which itself was pretty poor. The absolute worst model overall was the Quarterly-RDPI-Growth Predicted Model. I suspect that these models are not robust because there are only 18 or 19 (when including 2020) observations of election years off of which I am working. It is a pretty small sample size and difficult to draw statistically significant insights from. This reflects a challenge with using economic data to forecast elections—there are only so many elections to draw data from and to use to train models, resulting in a lot of variance as we see with my linear regression models. Across all models, I had errors that could have totally changed the outcome of who wins the popular vote. *How can we base a forecast on models that themselves cannot make a real prediction?*

In future economic models, I hope to use more granular data (month-wise or quarter-wise) and involve polling data to track how opinions change along with measures of economic performance. This time, I only used bivariate linear regressions, but I will in the future include multiple independent variables and weigh them by polls of voters and how salient they are.

##Sources##

“Presidential Debates Do Matter | 538 Politics Podcast.” *YouTube*, uploaded by FiveThirtyEight, 9 Sept. 2024, www.youtube.com/watch?v=PkjfKF0frvs.

Data Provided by GOV 1347: Election Analytics teaching staff (which itself drew from the Burueau of Economic Analysia and Federal Reserve Economic Data)
