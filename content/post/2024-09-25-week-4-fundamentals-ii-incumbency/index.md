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


``` r
####---------------------------------------------------------------------------------#
#### Descriptive statistics on the incumbency advantage. -- Code by Matthew Dardet
####---------------------------------------------------------------------------------#

# How many post-war elections (18 and 2024) have there been 
# where an incumbent president won? 
d_vote |> 
  filter(winner) |> 
  select(year, win_party = party, win_cand = candidate) |> 
  mutate(win_party_last = lag(win_party, order_by = year),
         win_cand_last = lag(win_cand, order_by = year)) |> 
  mutate(reelect_president = win_cand_last == win_cand) |> 
  filter(year > 1948 & year < 2024) |> 
  group_by(reelect_president) |> 
  summarize(N = n()) |> 
  mutate(Percent = round(N/sum(N) * 100, 2)) |>
  as.data.frame() |>
  kable(col.names = c("Incumbent President Re-elected",
                      "Count",
                      "Percentage")) |>
  kable_styling(bootstrap_options = "hover",
                position = "center")
```

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

``` r
# A different way of assessing the incumbency advantage 
# (out of 11 elections where there was at least one incumbent running). 
inc_tab <- d_vote |> 
  filter(year > 1948 & year < 2024) |>
  select(year, party, candidate, incumbent, winner) |> 
  pivot_wider(names_from = party, 
              values_from = c(candidate, incumbent, winner)) |> 
  filter(incumbent_DEM == TRUE | incumbent_REP == TRUE)


cat(paste0("Elections with At Least One Incumbent Running: ", nrow(inc_tab), "\n",
   "Incumbent Victories: ", (sum(inc_tab$incumbent_REP & inc_tab$winner_REP) + 
                             sum(inc_tab$incumbent_DEM & inc_tab$winner_DEM)), "\n",
    "Percentage: ", round((sum(inc_tab$incumbent_REP & inc_tab$winner_REP) + 
                           sum(inc_tab$incumbent_DEM & inc_tab$winner_DEM))/
                           nrow(inc_tab)*100, 2)))
```

```
## Elections with At Least One Incumbent Running: 11
## Incumbent Victories: 7
## Percentage: 63.64
```

``` r
# In the six elections since 2000?
inc_tab |> 
  filter(year >= 2000) |>
  kable(col.names = c("Election Year",
                      "Democratic Candidate",
                      "Republican Candidate",
                      "Democratic Incumbency",
                      "Republican Incumbency",
                      "Democratic Win",
                      "Republican Win")) |>
  kable_styling(bootstrap_options = "hover",
                position = "center")
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

``` r
# How many post-war elections have there been where the incumbent *party* won? 
d_vote |> 
  filter(winner) |> 
  select(year, win_party = party, win_cand = candidate) |> 
  mutate(win_party_last = lag(win_party, order_by = year),
         win_cand_last = lag(win_cand, order_by = year)) |> 
  mutate(reelect_party = win_party_last == win_party) |> 
  filter(year > 1948 & year < 2024) |> 
  group_by(reelect_party) |> 
  summarize(N = n()) |> 
  mutate(Percent = round(N/sum(N) * 100, 2)) |>
  as.data.frame() |>
  kable(col.names = c("Incumbent Party Re-elected",
                      "Count",
                      "Percentage")) |>
  kable_styling(bootstrap_options = "hover",
                position = "center")
```

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

``` r
# How many post-war elections have there been where winner served in 
# previous administration?
(100*round(prop.table(table(`prev_admin` = d_vote$prev_admin[d_vote$year > 1948 & 
                                     d_vote$year < 2024 & 
                                     d_vote$winner == TRUE])), 4)) |>
  kable(col.names = c("Previous Administration Member Elected",
                      "Percentage")) |>
  kable_styling(bootstrap_options = "hover",
                position = "center")
```

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


``` r
####----------------------------------------------------------#
#### Pork analysis. -- Code by Matthew Dardet
####----------------------------------------------------------#
 
# Read federal grants dataset from Kriner & Reeves (2008). 
d_pork_state <- read_csv("fedgrants_bystate_1988-2008.csv", show_col_types = FALSE)

# What strategy do presidents pursue? 
d_pork_state |> 
  filter(!is.na(state_year_type)) |> 
  group_by(state_year_type) |>
  summarize(mean_grant = mean(grant_mil, na.rm = T), se_grant = sd(grant_mil, na.rm = T)/sqrt(n())) |> 
  ggplot(aes(x = state_year_type, y = mean_grant, ymin = mean_grant-1.96*se_grant, ymax = mean_grant+1.96*se_grant)) + 
  coord_flip() + 
  geom_bar(stat = "identity", fill = "#85bb65") + 
  geom_errorbar(width = 0.2) + 
  labs(x = "Type of State & Year", 
       y = "Federal Grant Spending (Millions of $)", 
       title = "Federal Grant Spending by State Election Type") + 
  plot_theme()
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" />

``` r
# Do presidents strategize for their successor as well? 
d_pork_state |> 
  filter(!is.na(state_year_type2)) |> 
  group_by(state_year_type2) |>
  summarize(mean_grant = mean(grant_mil, na.rm = T), se_grant = sd(grant_mil, na.rm = T)/sqrt(n())) |> 
  ggplot(aes(x = state_year_type2, y = mean_grant, ymin = mean_grant-1.96*se_grant, ymax = mean_grant+1.96*se_grant)) + 
  coord_flip() + 
  geom_bar(stat = "identity", fill = "#85bb65") + 
  geom_errorbar(width = 0.2) + 
  labs(x = "Type of State & Year", 
       y = "Federal Grant Spending (Millions of $)", 
       title = "Federal Grant Spending by State Election Type") + 
  plot_theme()
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-2.png" width="672" />

``` r
# Pork county model. 
d_pork_county <- read_csv("fedgrants_bycounty_1988-2008.csv", show_col_types = FALSE)

pork_mod_county_1 <- lm(dvoteswing_inc  ~ dpct_grants*comp_state + as.factor(year), 
                      d_pork_county)
modelsummary(pork_mod_county_1, title = "Pork County-Level Model")
```

<table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
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

``` r
pork_mod_county_2 <- lm(dvoteswing_inc ~ dpct_grants*comp_state + as.factor(year) +
                          dpc_income + inc_ad_diff + inc_campaign_diff + 
                          dhousevote_inc + iraq_cas2004 + iraq_cas2008 + 
                          dpct_popl,
                        data = d_pork_county)
modelsummary(pork_mod_county_2, title = "Extended Pork County-Level Model")
```

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

``` r
# Pork state model. 
d_pork_state_model <- d_state_vote |>
  mutate(state_abb = state.abb[match(d_state_vote$state, state.name)]) |>
  inner_join(d_pork_state, by = c("year", "state_abb")) |>
  left_join(d_vote, by = "year") |>
  filter(incumbent_party == TRUE) |>
  mutate(inc_pv2p = ifelse(party == "REP", R_pv2p, D_pv2p)) |>
  mutate(is_comp = case_when(state_year_type == "swing + election year" ~ 1,
                             .default = 0)) |>
  group_by(state) |>
  mutate(change_grant_mil = (1-grant_mil/(lag(grant_mil, n = 1)))*100,
         change_inc_pv2p = (1-inc_pv2p/(lag(inc_pv2p, n = 1)))*100) |>
  ungroup() |>
  select(state, year, is_comp, change_grant_mil, change_inc_pv2p)

pork_state_mod <- lm(change_inc_pv2p ~ is_comp*change_grant_mil + as.factor(year),
                     data = d_pork_state_model)
modelsummary(pork_state_mod, title = "Pork State-Level Model")
```

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

One model of the incumbency advantage is Alan Abramowitz's **Time for Change** model, which he developed in 1988. It is a simple Ordinary Least Squares Regression Model that relies on three independent variables:  GDP Growth for Quarter 2, June Gallup Poll Approval, and a binary variable on incumbency status of a candidate. 


``` r
####----------------------------------------------------------#
#### Time for a change model applied to 2024
####----------------------------------------------------------#
# Evaluate models and compare them to your own models/predictions. 
# juneapp for Biden might be affected by the fact he was still running


# Create comprehensive dataset to involve econ and vote data
econ_vote <- d_vote |>
  left_join(d_econ, by="year")

# Now narrow down econ and vote data to just incumbents 
incumb_econ_vote <- econ_vote |>
  filter(incumbent_party) |>
  mutate(incumbent = as.numeric(incumbent))

# Train data on previous election (excluding 2020)
train_for_2024_exc <- incumb_econ_vote |>
  filter(year < 2020)
test_for_2024_exc <- incumb_econ_vote |>
  filter(year == 2024)

# Train data on previous election (including 2020)
train_for_2024_inc <- incumb_econ_vote |>
  filter(year < 2024)
test_for_2024_inc <- incumb_econ_vote |>
  filter(year == 2024)

# Construct linear regression based on TFC -- Exc
tfc_mod_2024_exc <- lm(pv2p ~ GDP_growth_quarterly + incumbent + juneapp, 
                   data = train_for_2024_exc)
# modelsummary(tfc_mod_2024_exc, title = "Time for Change Model for 2024",
#              notes = "Excluding 2020 Training Data",
#              coef_rename = c("GDP_growth_quarterly" = "GDP Growth (Quarterly)",
#                              "incumbent" = "Incumbency Status",
#                              "juneapp" = "Approval Rating in June"))

# Construct linear regression based on TFC -- Inc
tfc_mod_2024_inc <- lm(pv2p ~ GDP_growth_quarterly + incumbent + juneapp, 
                   data = train_for_2024_inc)
# modelsummary(tfc_mod_2024_inc, title = "Time for Change Model for 2024",
#              notes = "Including 2020 Training Data",
#              coef_rename = c("GDP_growth_quarterly" = "GDP Growth (Quarterly)",
#                              "incumbent" = "Incumbency Status",
#                              "juneapp" = "Approval Rating in June"))
# Predict for Harris as incumbent
harris_pv2p_exc <- predict(tfc_mod_2024_exc,
                       newdata = test_for_2024_exc)
harris_pv2p_inc <- predict(tfc_mod_2024_inc,
                       newdata = test_for_2024_inc)


# HYPOTHETICAL: HARRIS IS NOT REALLY AN INCUMBENT AND NEITHER IS TRUMP. TREAT AS NON-INCUMBENT ELECTION
incumb_econ_vote_hyp <- econ_vote |>
  filter(incumbent_party) |>
  mutate(incumbent = as.numeric(incumbent)) |>
  mutate(incumbent = if_else(year == 2024, 0, incumbent))

# HYP: Train data on previous election (excluding 2020)
train_for_2024_hyp_exc <- incumb_econ_vote_hyp |>
  filter(year < 2020)
test_for_2024_hyp_exc <- incumb_econ_vote_hyp |>
  filter(year == 2024)

# HYP: Train data on previous election (including 2020)
train_for_2024_hyp_inc <- incumb_econ_vote_hyp |>
  filter(year < 2024)
test_for_2024_hyp_inc <- incumb_econ_vote_hyp |>
  filter(year == 2024)

# HYP: Construct linear regression based on TFC - Excluding 2020
tfc_mod_2024_hyp_exc <- lm(pv2p ~ GDP_growth_quarterly + incumbent + juneapp, 
                   data = train_for_2024_hyp_exc)
# modelsummary(tfc_mod_2024_hyp_exc, title = "Time for Change Model for 2024",
#              notes = "Excluding 2020 Training Data",
#              coef_rename = c("GDP_growth_quarterly" = "GDP Growth (Quarterly)",
#                              "incumbent" = "Incumbency Status",
#                              "juneapp" = "Approval Rating in June"))
# HYP: Construct linear regression based on TFC - Including 2020
tfc_mod_2024_hyp_inc <- lm(pv2p ~ GDP_growth_quarterly + incumbent + juneapp, 
                   data = train_for_2024_hyp_inc)
# modelsummary(tfc_mod_2024_hyp_inc, title = "Time for Change Model for 2024",
#              notes = "Including 2020 Training Data",
#              coef_rename = c("GDP_growth_quarterly" = "GDP Growth (Quarterly)",
#                              "incumbent" = "Incumbency Status",
#                              "juneapp" = "Approval Rating in June"))
# HYP: Now Predict
harris_pv2p_hyp_exc <- predict(tfc_mod_2024_hyp_exc,
                       newdata = test_for_2024_hyp_exc)
harris_pv2p_hyp_inc <- predict(tfc_mod_2024_hyp_inc,
                       newdata = test_for_2024_hyp_inc)

####----------------------------------------------------------#
#### VIEWING ALL MODELS TOGETHER
####----------------------------------------------------------#

tfc_models_2024 <- list(
  "Excluding 2020 Data" = tfc_mod_2024_exc,
  "Including 2020 Data" = tfc_mod_2024_inc,
  "Harris Non-Incumbent Hypothetical, Excluding 2020" = tfc_mod_2024_hyp_exc,
  "Harris Non-Incumbent Hypothetical, Including 2020" = tfc_mod_2024_hyp_inc)
modelsummary(tfc_models_2024,
             title = "Time for Change Models for 2024",
             coef_rename = c("GDP_growth_quarterly" = "GDP Growth (Quarterly)",
                             "incumbent" = "Incumbency Status",
                             "juneapp" = "Approval Rating in June"))
```

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

``` r
# harris_pv2p_exc
# harris_pv2p_inc
# harris_pv2p_hyp_exc
# harris_pv2p_hyp_inc

tfc_predicted_vs <- data.frame(
  candidate = c("Kamala Harris", "Donald Trump"),
  pv2p_exc = c(harris_pv2p_exc, (100-harris_pv2p_exc)),
  pv2p_inc = c(harris_pv2p_inc, (100-harris_pv2p_inc)),
  pv2p_hyp_exc = c(harris_pv2p_hyp_exc, (100-harris_pv2p_hyp_exc)),
  pv2p_hyp_inc = c(harris_pv2p_hyp_inc, (100-harris_pv2p_hyp_inc)),
  pv2p_silver_model = c(51.31497, 48.06832) # Drawn from calculations of two-party vote share, using prediction on Nate Silver's ensemble model that weighs polls closer to election day but also involves economic data; see week 3 code for more details and for verification on accuracy
)

# kable(tfc_predicted_vs,
#       digits = 2,
#       format = "html",
#       col.names = c("Candidate",
#                     "Excluding 2020 Data",
#                     "Including 2020 Data",
#                     "Harris Non-Incumbent Hypothetical, Excluding 2020",
#                     "Harris Non-Incumbent Hypothetical, Including 2020",
#                     "Silver's Ensemble Model, Weighing Polls Closer to Election Day"),
#       caption = "Two-Party Vote Shares (%) Across Various Time for Change Models"
# ) |>
#   kable_styling(bootstrap_options = "hover",
#                 position = "center")

# Just for fun: Create a function that colors the 2-party vote share winners to make visualization more readable
color_cells <- function(candidate, value) {
  value <- round(value, 2)
  if(
    candidate == "Kamala Harris" & value > 50) {
    return(cell_spec(value, "html", color = "white", background = "steelblue3"))
  } else if (candidate == "Donald Trump" & value > 50) {
    return(cell_spec(value, "html", color = "white", background = "tomato3"))
  } else {
    return(value)
  }
}

# Now apply the color function 
tfc_predicted_vs_kable <- tfc_predicted_vs |>
  mutate(across(-candidate, 
                ~ mapply(color_cells, candidate, .)))

# Construct the table using kable
kable(tfc_predicted_vs_kable, escape = FALSE, format = "html", 
      caption = "Two-Party Vote Shares (%) Across Various Time for Change Models",
      col.names = c("Candidate",
                    "Excluding 2020 Data",
                    "Including 2020 Data",
                    "Harris Non-Incumbent Hypothetical, Excluding 2020",
                    "Harris Non-Incumbent Hypothetical, Including 2020",
                    "Silver's Ensemble Model, Weighing Polls Closer to Election Day")) |>
  kable_styling(bootstrap_options = "hover", position = "center")
```

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

Abramowitz, Alan I. “An Improved Model for Predicting Presidential Election Outcomes.” *PS: Political Science and Politics*, vol. 21, no. 4, 1988, pp. 843–47. JSTOR, https://doi.org/10.2307/420023. 

Kriner, Douglas L., and Andrew Reeves. “Presidential Particularism and Divide-the-Dollar Politics.” *American Political Science Review* 109.1 (2015): 155–171. Web.

Olmsted, Edith. “Trump Has a Wild New Theory for His Flagging Crowd Sizes.” *The New Republic*, 30 Sept. 2024, <https://newrepublic.com/post/186504/donald-trump-joe-biden-theory-crowd-sizes.>

“When and Where Is the Vance-Walz US Vice Presidential Debate?” *Reuters*, 19 Sept. 2024, [www.reuters.com/world/us/when-where-is-vance-walz-us-vice-presidential-debate-2024-09-19/](http://www.reuters.com/world/us/when-where-is-vance-walz-us-vice-presidential-debate-2024-09-19/).

Polling Data Provided by GOV 1347: Election Analytics teaching staff (which itself drew from the FiveThirtyEight GitHub)

Economic Data Provided by GOV 1347: Election Analytics teaching staff (which itself drew from the Burueau of Economic Analysia and Federal Reserve Economic Data)
