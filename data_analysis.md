---
title: "Combining Data and Analysis"
author: "Daniel Fuller"
date: "2024-05-30"
output:
  html_document:
    keep_md: yes
---



## Read Data


```r
barrhaven <- read_csv("ottawa_barrhaven_bike_transit_drive.csv")
blair <- read_csv("ottawa_blaire_bike_transit_drive.csv")
```

## Joining Data


```r
data <- bind_rows(barrhaven, blair)
```

## Summary statistics by mode


```r
rm_covsum(data=data, maincov = 'mode',
covs=c('distance_km','duration_hours'))
```

<table class="table" style="margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;">  </th>
   <th style="text-align:right;"> Full Sample (n=184) </th>
   <th style="text-align:right;"> bike (n=46) </th>
   <th style="text-align:right;"> bike transit (n=46) </th>
   <th style="text-align:right;"> car (n=46) </th>
   <th style="text-align:right;"> transit (n=46) </th>
   <th style="text-align:right;"> p-value </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> <span style="font-weight: bold;">distance km</span> </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;"> 0.083 </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Mean (sd) </td>
   <td style="text-align:right;"> 18.4 (8.3) </td>
   <td style="text-align:right;"> 16.1 (7.1) </td>
   <td style="text-align:right;"> 19.4 (6.7) </td>
   <td style="text-align:right;"> 18.4 (9.5) </td>
   <td style="text-align:right;"> 19.5 (9.4) </td>
   <td style="text-align:right;">  </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Median (Min,Max) </td>
   <td style="text-align:right;"> 15.8 (5.5, 38.5) </td>
   <td style="text-align:right;"> 14.7 (5.5, 27.6) </td>
   <td style="text-align:right;"> 15.1 (10.2, 29.4) </td>
   <td style="text-align:right;"> 15.9 (6.1, 37.9) </td>
   <td style="text-align:right;"> 18.2 (5.6, 38.5) </td>
   <td style="text-align:right;">  </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="font-weight: bold;">duration hours</span> </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;"> <span style="font-weight: bold;"> </span>
</td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Mean (sd) </td>
   <td style="text-align:right;"> 0.7 (0.4) </td>
   <td style="text-align:right;"> 0.9 (0.4) </td>
   <td style="text-align:right;"> 0.5 (0.2) </td>
   <td style="text-align:right;"> 0.3 (0.1) </td>
   <td style="text-align:right;"> 1.1 (0.4) </td>
   <td style="text-align:right;">  </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Median (Min,Max) </td>
   <td style="text-align:right;"> 0.6 (0.2, 2.7) </td>
   <td style="text-align:right;"> 0.9 (0.3, 1.5) </td>
   <td style="text-align:right;"> 0.5 (0.2, 1.2) </td>
   <td style="text-align:right;"> 0.3 (0.2, 0.5) </td>
   <td style="text-align:right;"> 1.0 (0.6, 2.7) </td>
   <td style="text-align:right;">  </td>
  </tr>
</tbody>
</table>

## Summary statistics by station


```r
rm_covsum(data=data, maincov = 'station',
covs=c('distance_km','duration_hours'))
```

<table class="table" style="margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;">  </th>
   <th style="text-align:right;"> Full Sample (n=184) </th>
   <th style="text-align:right;"> Barrhaven Center Station, Ottawa, Canada (n=88) </th>
   <th style="text-align:right;"> Blair Station, Ottawa, Canada (n=96) </th>
   <th style="text-align:right;"> p-value </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> <span style="font-weight: bold;">distance km</span> </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;"> <span style="font-weight: bold;"> </span>
</td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Mean (sd) </td>
   <td style="text-align:right;"> 18.4 (8.3) </td>
   <td style="text-align:right;"> 26.1 (4.5) </td>
   <td style="text-align:right;"> 11.3 (3.1) </td>
   <td style="text-align:right;">  </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Median (Min,Max) </td>
   <td style="text-align:right;"> 15.8 (5.5, 38.5) </td>
   <td style="text-align:right;"> 25.7 (16.5, 38.5) </td>
   <td style="text-align:right;"> 11.2 (5.5, 20.2) </td>
   <td style="text-align:right;">  </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="font-weight: bold;">duration hours</span> </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;"> <span style="font-weight: bold;"> </span>
</td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Mean (sd) </td>
   <td style="text-align:right;"> 0.7 (0.4) </td>
   <td style="text-align:right;"> 0.9 (0.5) </td>
   <td style="text-align:right;"> 0.6 (0.3) </td>
   <td style="text-align:right;">  </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Median (Min,Max) </td>
   <td style="text-align:right;"> 0.6 (0.2, 2.7) </td>
   <td style="text-align:right;"> 0.9 (0.2, 2.7) </td>
   <td style="text-align:right;"> 0.6 (0.2, 2.5) </td>
   <td style="text-align:right;">  </td>
  </tr>
</tbody>
</table>

## Data Viz by time


```r
ggplot(data, aes(x = duration_hours, y = mode, fill = mode)) +
  geom_density_ridges() + 
  stat_density_ridges(quantile_lines = TRUE, alpha = 0.75, quantiles = 2) +
  facet_wrap(~ station)
```

![](data_analysis_files/figure-html/unnamed-chunk-5-1.png)<!-- -->


