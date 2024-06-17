---
title: "Combining Data and Analysis"
author: "Daniel Fuller"
date: "2024-05-30"
output:
  html_document:
    keep_md: true
  pdf_document: default
  word_document: default
---



## Read Data


```r
barrhaven <- read_csv("Ottawa/ottawa_barrhaven_bike_transit_drive.csv")
blair <- read_csv("Ottawa/ottawa_blaire_bike_transit_drive.csv")
scar <- read_csv("Toronto/toronto_scarborough_bike_transit_drive.csv")
vaughn <- read_csv("Toronto/toronto_vaughn_bike_transit_drive.csv")
bross <- read_csv("Montreal/montreal_brossard_bike_transit_drive.csv")
rivier <- read_csv("Montreal/montreal_riviereprairie_bike_transit_drive.csv")
mckenzie <- read_csv("Calgary/calgary_mckenzie_bike_transit_drive.csv")
np <- read_csv("Calgary/calgary_northpoint_bike_transit_drive.csv")
heritage <- read_csv("Edmonton/edmonton_heritage_bike_transit_drive.csv")
naki <- read_csv("Edmonton/edmonton_naki_bike_transit_drive.csv")
surrey <- read_csv("Vancouver/vancouver_surrey_bike_transit_drive.csv")
bridge <- read_csv("Vancouver/vancouver_bridgeport_bike_transit_drive.csv")
```

## Joining Data


```r
data <- bind_rows(barrhaven, blair, scar, vaughn, bross, rivier, mckenzie, np, heritage, naki, surrey, bridge)

write_csv(data, file = "mode_city_data.csv")
```

## Summary statistics by mode


```r
rm_covsum(data=data, maincov = 'mode',
covs=c('distance_km','duration_hours'))
```

<table class="table" style="color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;">  </th>
   <th style="text-align:right;"> Full Sample (n=1132) </th>
   <th style="text-align:right;"> bike (n=283) </th>
   <th style="text-align:right;"> bike transit (n=283) </th>
   <th style="text-align:right;"> car (n=283) </th>
   <th style="text-align:right;"> transit (n=283) </th>
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
   <td style="text-align:right;"> <span style="font-weight: bold;"> </span>
</td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Mean (sd) </td>
   <td style="text-align:right;"> 22.1 (7.7) </td>
   <td style="text-align:right;"> 20.4 (6.8) </td>
   <td style="text-align:right;"> 25.0 (7.4) </td>
   <td style="text-align:right;"> 21.8 (9.0) </td>
   <td style="text-align:right;"> 21.0 (6.8) </td>
   <td style="text-align:right;">  </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Median (Min,Max) </td>
   <td style="text-align:right;"> 21.5 (5.5, 46.4) </td>
   <td style="text-align:right;"> 19.9 (5.5, 38.2) </td>
   <td style="text-align:right;"> 25.2 (10.2, 45.2) </td>
   <td style="text-align:right;"> 20.1 (5.7, 45.3) </td>
   <td style="text-align:right;"> 20.7 (5.6, 46.4) </td>
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
   <td style="text-align:right;"> 0.8 (0.5) </td>
   <td style="text-align:right;"> 1.2 (0.4) </td>
   <td style="text-align:right;"> 0.6 (0.3) </td>
   <td style="text-align:right;"> 0.5 (0.1) </td>
   <td style="text-align:right;"> 1.1 (0.5) </td>
   <td style="text-align:right;">  </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Median (Min,Max) </td>
   <td style="text-align:right;"> 0.7 (0.1, 5.1) </td>
   <td style="text-align:right;"> 1.1 (0.3, 2.4) </td>
   <td style="text-align:right;"> 0.6 (0.1, 2.1) </td>
   <td style="text-align:right;"> 0.5 (0.2, 0.8) </td>
   <td style="text-align:right;"> 1.1 (0.4, 5.1) </td>
   <td style="text-align:right;">  </td>
  </tr>
</tbody>
</table>

## Summary statistics by station


```r
rm_covsum(data=data, maincov = 'station',
covs=c('distance_km','duration_hours'))
```

<table class="table" style="color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;">  </th>
   <th style="text-align:right;"> Full Sample (n=1132) </th>
   <th style="text-align:right;"> Barrhaven Center Station, Ottawa, Canada (n=88) </th>
   <th style="text-align:right;"> Blair Station, Ottawa, Canada (n=96) </th>
   <th style="text-align:right;"> Bridgeport Station, Vancouver, Canada (n=96) </th>
   <th style="text-align:right;"> Brossard Station, Montreal, Canada (n=80) </th>
   <th style="text-align:right;"> Heritage Valley Station, Edmonton, Canada (n=96) </th>
   <th style="text-align:right;"> McKenzie Towne, Calgary, Canada (n=96) </th>
   <th style="text-align:right;"> Naki Transit Centre, Edmonton, Canada (n=96) </th>
   <th style="text-align:right;"> North Pointe Transit Terminal, Calgary, Canada (n=96) </th>
   <th style="text-align:right;"> Riviere-des-Prairies Station, Montreal, Canada (n=100) </th>
   <th style="text-align:right;"> Scarborough GO Station, Toronto, Canada (n=92) </th>
   <th style="text-align:right;"> Surrey Central Station, Surrey, Canada (n=96) </th>
   <th style="text-align:right;"> Vaughan Metropolitan Centre Station, Toronto, Canada (n=100) </th>
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
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
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
   <td style="text-align:right;"> 22.1 (7.7) </td>
   <td style="text-align:right;"> 26.1 (4.5) </td>
   <td style="text-align:right;"> 11.3 (3.1) </td>
   <td style="text-align:right;"> 14.0 (3.6) </td>
   <td style="text-align:right;"> 22.4 (5.0) </td>
   <td style="text-align:right;"> 22.1 (4.2) </td>
   <td style="text-align:right;"> 25.2 (4.3) </td>
   <td style="text-align:right;"> 17.5 (4.1) </td>
   <td style="text-align:right;"> 20.3 (4.9) </td>
   <td style="text-align:right;"> 24.5 (5.2) </td>
   <td style="text-align:right;"> 17.8 (3.5) </td>
   <td style="text-align:right;"> 33.6 (5.7) </td>
   <td style="text-align:right;"> 29.5 (7.0) </td>
   <td style="text-align:right;">  </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Median (Min,Max) </td>
   <td style="text-align:right;"> 21.5 (5.5, 46.4) </td>
   <td style="text-align:right;"> 25.7 (16.5, 38.5) </td>
   <td style="text-align:right;"> 11.2 (5.5, 20.2) </td>
   <td style="text-align:right;"> 15.1 (5.7, 23.0) </td>
   <td style="text-align:right;"> 21.9 (12.2, 35.5) </td>
   <td style="text-align:right;"> 21.9 (15.0, 46.4) </td>
   <td style="text-align:right;"> 25.7 (13.6, 35.9) </td>
   <td style="text-align:right;"> 18.7 (7.1, 26.5) </td>
   <td style="text-align:right;"> 19.9 (10.6, 32.8) </td>
   <td style="text-align:right;"> 24.6 (16.3, 43.2) </td>
   <td style="text-align:right;"> 18.5 (10.7, 29.8) </td>
   <td style="text-align:right;"> 33.2 (22.4, 45.2) </td>
   <td style="text-align:right;"> 28.2 (16.6, 45.3) </td>
   <td style="text-align:right;">  </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="font-weight: bold;">duration hours</span> </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
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
   <td style="text-align:right;"> 0.8 (0.5) </td>
   <td style="text-align:right;"> 0.9 (0.5) </td>
   <td style="text-align:right;"> 0.6 (0.3) </td>
   <td style="text-align:right;"> 0.7 (0.4) </td>
   <td style="text-align:right;"> 0.8 (0.4) </td>
   <td style="text-align:right;"> 0.9 (0.6) </td>
   <td style="text-align:right;"> 1.0 (0.6) </td>
   <td style="text-align:right;"> 0.8 (0.3) </td>
   <td style="text-align:right;"> 0.8 (0.4) </td>
   <td style="text-align:right;"> 1.0 (0.5) </td>
   <td style="text-align:right;"> 0.8 (0.3) </td>
   <td style="text-align:right;"> 1.1 (0.6) </td>
   <td style="text-align:right;"> 0.9 (0.4) </td>
   <td style="text-align:right;">  </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Median (Min,Max) </td>
   <td style="text-align:right;"> 0.7 (0.1, 5.1) </td>
   <td style="text-align:right;"> 0.9 (0.2, 2.7) </td>
   <td style="text-align:right;"> 0.6 (0.2, 2.5) </td>
   <td style="text-align:right;"> 0.6 (0.2, 3.3) </td>
   <td style="text-align:right;"> 0.8 (0.2, 2.1) </td>
   <td style="text-align:right;"> 0.8 (0.1, 5.1) </td>
   <td style="text-align:right;"> 0.9 (0.1, 3.6) </td>
   <td style="text-align:right;"> 0.8 (0.1, 1.8) </td>
   <td style="text-align:right;"> 0.8 (0.2, 2.0) </td>
   <td style="text-align:right;"> 0.9 (0.2, 2.2) </td>
   <td style="text-align:right;"> 0.7 (0.2, 1.4) </td>
   <td style="text-align:right;"> 1.0 (0.2, 2.4) </td>
   <td style="text-align:right;"> 0.8 (0.1, 1.9) </td>
   <td style="text-align:right;">  </td>
  </tr>
</tbody>
</table>

## Data Viz by time


```r
viz <- ggplot(data, aes(x = duration_hours, y = mode, fill = mode)) +
  geom_density_ridges() + 
  stat_density_ridges(quantile_lines = TRUE, alpha = 0.75, quantiles = 2) +
  facet_wrap(~ station)
plot(viz)
```

![](data_analysis_files/figure-html/unnamed-chunk-5-1.png)<!-- -->


