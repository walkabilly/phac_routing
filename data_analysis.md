---
title: "Combining Mass Rapid Transit and Active Transportation for Physical Activity Promotion"
author: "Daniel Fuller"
date: "2024-05-30"
output:
  html_document:
    keep_md: true
  pdf_document: default
  word_document: default
---



## Introduction

Active transportation (AT) is one of the four domains of physical activity and is associated with higher levels of total physical activity. Consequently, it is an important behaviour to target for health promotion and chronic disease prevention. AT is particularly attractive as a target for physical activity promotion, given that individuals generally travel to various destinations throughout the day. By replacing sedentary forms of transportation (such as motor vehicle use) with active forms of transportation (such as cycling or walking), Canadians can increase their physical activity levels. Moreover, walking and especially cycling for transportation are often carried out at intensitieis of physical activity (i.e., moderate-to-vigourous intensity) that contribute towards meeting the physical activity recommendation from the the Canadian 24-Hour Movement Guidelines.

Typically, people opt for active modes of transportation for travelling shorter distances (i.e. to and from a local shop or public transit stop). Using origin-destination survey data in Montreal, it was found that the 85th percentile of trip distance for walking to various destinations was under 2 kilometers, and for cycling it was less than 6.5 kilometers (Yasmin, F. et. al., 2010, Larsen J, 2010). This is an important consideration for the promotion of AT. Although within smaller cities, large portions of the population live within these distances of frequently visited destinations, in larger cities, there are often substantial numbers of residents living much further from these destinations in the central business district (CBD). Promoting AT to cover large distances is unlikely to be successful if the messaging suggests that they should walk or bike the entire trip. However, many recent investments in Canada have been made to expand mass rapid transit (MRT) systems (including subways, light rail and bus rapid transit). This expansion has brought higher speed transit and stations closer to suburban neighbourhoods and is often faster than the stop and start nature of typical bus routes.

In many countries with more mature MRT systems, it is common to see bikes parked at transit stations with commuters continuing their journey by bus or rail. Theoretically, such transportation choices are becoming increasingly available to more Canadians as new commuter rail, subway, Light Rapid Transit, and Bus Rapid Transit become available in large Canadian cities. Although some of the supporting infrastructure of secure bike parking and easy walking and cycling sidewalks and bikeways are not yet available, those infrastructure expenses are a fraction of the cost of the MRT projects themselves. A key question to consider before developing policy aimed at getting people to use more AT, is how do trips incorporating AT to MRT compare to those completed entirely by car and/or entirely by transit? To determine this, it is important to understand how the duration of trips to MRT by walking or cycling compare to trips taken entirely by transit or entirely by driving.

Driving has the advantage of direct transportation from home to destination, but often the disadvantage of traffic congestion and the costs of operating a vehicle and parking. While MRT is often undeterred by traffic congestion, there are often multiple legs to a trip, e.g. walking to a bus stop, waiting for a bus, travelling to a MRT station, which can make transit use a longer trip than driving. However, by investigating the potentional of taking AT to the MRT to replace the local bus portion of trips, we may see that this can reduce some of the time taken by some of the legs of the trip in cases where individuals can walk to the station, or cycle to it from a few kilometers away, AND increase physical activity levels. 

## Objective

To compare travel distance and physical activity amounts attained from point-to-point travel by automobile to CBD station, bus to MRT to CBD station, and by AT to MRT to CBD station.

## Methods

This used the [Google Route API](https://mapsplatform.google.com/maps-products/routes/) implemented in the [googleway R package](https://www.rdocumentation.org/packages/googleway/versions/2.7.8) to to compare travel time, travel distance, and estimated physical activity contribution of trips from 25 randomly selected street addresses within a 5km buffer of these two stations to the downtown central business districts (CBD) of 6 major Canadian cities. The modes of transportation used for the trip calculations were

* Transit Only
    * Time and distance calculations include walking to and from stations
* Bike 
* Bike + Transit 
    * Bike to main station and transit to destination
* Drive 

### Origin  - Station Selection 

Each station was selected based on distance from the city center, proximity to a transit station, and discussion with staff at PHAC. This was not an exact science but meant to represent a selection of 2 stations per city to a sense of travel times and distances for different modes of transportation. The selected stations are as follows

1. Ottawa
    * Blair Station
    * Barrhaven
2. Montreal 
    * Brossard Station
    * Rivière-des-Prairies Station
3. Toronto
    * Vaughan Metropolitan Centre Stations
    * Scarborough GO Station
4. Vancouver
    * Surrey Central Station
    * Bridgeport Station
5. Edmonton
    * Heritage Valley Station
    * Nakî Transit Centre & Park and Ride
6. Calgary
    * North Pointe Transit Terminal
    * McKenzie Towne

### Destination - City center 

Destinations were selected for each city. Each destination was either a major Art Gallery or Library located in the city of each city. These locations were selected because they are public, are located downtown, and draw considerable numbers of people. The destination locations are as follows

1. Ottawa
    * National Gallery of Canada
2. Montreal 
    * Musee d'art contemporain de Montreal
3. Toronto
    * Art Gallery of Ontario
4. Vancouver
    * Vancouver Art Gallery
5. Edmonton
    * Edmonton Public Library - Stanley A. Milner Library
6. Calgary
    * Calgary Public Library - Central Library

### Buffer and Home Selection

For each origin at a station, a 5km diameter buffer is drawn around the station. Within that 5km buffer, 25 points (ie., lat lon coordinates) are randomly selected using a seed to ensure reproducibility. A different seed is used for each station. Below is an example of the buffer and 25 points selected for the Ottawa Barrhaven Station.

##### Figure 1. 5km buffer around Barrhaven Station in Ottawa.   

![](barrhaven_buffer.png)


##### Figure 2. Randomly selected points within the 5km buffer around Barrhaven station.  

![](buffer_points.png)

For each trip type (i.e., Transit Only, Bike, Bike + Transit, and Drive) the `googleway` R package is used to generate trips from the randomly generated points to the destination. All trips are scheduled to arrive at the destination at 8:30am on either Tuesday June 11th or Tuesday June 25th. For the Bike + Transit trips, two trips are generated. First, a trip from the randomly selected point to the station of interest by bicycle, then a trip from the station of interest to the destination by transit. 

##### Figure 3. Googleway transit routes from randomly selected points to destination.  

![](barrhaven_routes.png)
Once all of the routes were calculated the travel time and travel distance elements were extracted from each trip type and each route and organized into a tidy dataset. On average there were 25 routes per trip type, however, on some occasions some routes failed to geocode. Table 1 presents the city, station, and trip type sample sizes for all cities. 

## Read Data



## Joining Data


```r
data <- bind_rows(barrhaven, blair, scar, vaughn, bross, rivier, mckenzie, np, heritage, naki, surrey, bridge)

write_csv(data, file = "mode_city_data.csv")
```


```r
summary_data <- data %>% 
  group_by(station) %>%
    summarize(n = n())
```



##### Figure 1. Number of observations per station   

| Station | Number of observations |                                         
| ------- | ---------------------- | 
| Barrhaven Center Station, Ottawa, Canada | 88 |           
| Blair Station, Ottawa, Canada | 96 |                       
| Bridgeport Station, Vancouver, Canada | 96 |                 
| Surrey Central Station, Surrey, Canada | 96 |   
| Heritage Valley Station, Edmonton, Canada | 96 |           
| Naki Transit Centre, Edmonton, Canada | 96 |              
| North Pointe Transit Terminal, Calgary, Canada | 96 |   
| McKenzie Towne, Calgary, Canada | 96 |   
| Brossard Station, Montreal, Canada | 80 |    
| Riviere-des-Prairies Station, Montreal, Canada | 100 |        
| Scarborough GO Station, Toronto, Canada | 92 |              
| Vaughan Metropolitan Centre Station, Toronto, Canada | 100 |  

# Analysis

Descriptive analysis will be conducted to describe the trip time and distance for all stations and cities together, then separately for individual cities. No statistical tests will be performed. 

##### Table 2. Descriptive statisics for travel time and mode by trip type by city


```r
rm_covsum(data=data, maincov = 'station', pvalue = FALSE,
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
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Mean (sd) </td>
   <td style="text-align:right;"> 22.2 (7.8) </td>
   <td style="text-align:right;"> 28.1 (4.3) </td>
   <td style="text-align:right;"> 11.5 (3.4) </td>
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
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Median (Min,Max) </td>
   <td style="text-align:right;"> 21.6 (5.3, 46.4) </td>
   <td style="text-align:right;"> 28.1 (19.1, 40.8) </td>
   <td style="text-align:right;"> 11.4 (5.3, 20.1) </td>
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
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Mean (sd) </td>
   <td style="text-align:right;"> 0.8 (0.5) </td>
   <td style="text-align:right;"> 0.9 (0.5) </td>
   <td style="text-align:right;"> 0.6 (0.4) </td>
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
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Median (Min,Max) </td>
   <td style="text-align:right;"> 0.7 (0.1, 5.1) </td>
   <td style="text-align:right;"> 0.9 (0.2, 2.8) </td>
   <td style="text-align:right;"> 0.6 (0.2, 2.7) </td>
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
  </tr>
</tbody>
</table>

Across of the stations the longest travel time on average was Surrey Central Station with an average travel time of 66 minutes. McKenzie Town in Calgary and Riviere-des-Prairies in Montreal also had average travel times of 60 minutes. The shortest average travel times were Blair Station in Ottawa and Brossard Station in Montreal with average travel times being 36 minutes. It should be noted that the stations we selected were chosen to be relatively far from the downtown, with an average of distance of 22.2km and a range of 5.3km to 46.4km. 

##### Table 3. Descriptive statisics for travel time and mode by trip type


```r
rm_covsum(data=data, maincov = 'mode', pvalue = FALSE,
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
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Mean (sd) </td>
   <td style="text-align:right;"> 22.2 (7.8) </td>
   <td style="text-align:right;"> 20.6 (7.0) </td>
   <td style="text-align:right;"> 25.3 (7.3) </td>
   <td style="text-align:right;"> 22.1 (9.1) </td>
   <td style="text-align:right;"> 21.0 (6.8) </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Median (Min,Max) </td>
   <td style="text-align:right;"> 21.6 (5.3, 46.4) </td>
   <td style="text-align:right;"> 20.0 (5.3, 38.2) </td>
   <td style="text-align:right;"> 25.5 (11.3, 45.2) </td>
   <td style="text-align:right;"> 20.3 (5.7, 45.3) </td>
   <td style="text-align:right;"> 20.6 (5.8, 46.4) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="font-weight: bold;">duration hours</span> </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
   <td style="text-align:right;">  </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Mean (sd) </td>
   <td style="text-align:right;"> 0.8 (0.5) </td>
   <td style="text-align:right;"> 1.2 (0.4) </td>
   <td style="text-align:right;"> 0.6 (0.3) </td>
   <td style="text-align:right;"> 0.5 (0.1) </td>
   <td style="text-align:right;"> 1.2 (0.5) </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Median (Min,Max) </td>
   <td style="text-align:right;"> 0.7 (0.1, 5.1) </td>
   <td style="text-align:right;"> 1.2 (0.3, 2.4) </td>
   <td style="text-align:right;"> 0.6 (0.1, 2.1) </td>
   <td style="text-align:right;"> 0.5 (0.2, 0.8) </td>
   <td style="text-align:right;"> 1.1 (0.4, 5.1) </td>
  </tr>
</tbody>
</table>

On average across all modes the trip duration was 48 minutes with a mean distance of 22.2km. On average car trips were the fastest at 30 minutes on average and a mean distance of 22.1km. The next fastest trip mode was biking to transit with an average time of 36 minutes and distance of 25.3km. Transit and cycling the entire distance had similar times with average travel times of 72 minutes. 

##### Figure 4. Visualization of travel time by mode and city


```r
viz <- ggplot(data, aes(x = duration_hours, y = mode, fill = mode)) +
  geom_density_ridges() + 
  stat_density_ridges(quantile_lines = TRUE, alpha = 0.75, quantiles = 2) +
  labs(
  x = "Duration in Hours",
  y = "Travel Mode",
  fill = "Travel Mode") +
  facet_wrap(~ station_name)
plot(viz)
```

![](data_analysis_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

The `joy plot` shows a histogram for travel time for each travel mode and each station. In general, the car travel mode has the shortest travel time and the most narrow range of the distribution. This suggests that driving is the fastest travel mode and the most consistent in terms of time. The next fastest travel mode was bike + transit, which was generally similar in travel time to driving except for the McKenzie Towne (Calgary), Blair (Ottawa), and Naki Transit Center (Calgary) stations. The distribution of the bike + transit travel times was wider for bike + transit compared to driving. Taking transit was rarely competitive with driving or biking + transit. The closest transit time between bike, bike + transit, and car was Surrey Central station. For transit use, the distribution was very wide, particularly for McKenzie Towne and Heritage Valley. Finally, simply cycling the entire distance was 

## Conclusion

Based on the analysis, overall cycling plus using transit to get from suburban areas appears to be competitive with driving and is faster than taking transit only or cycling the entire distance. The time difference across all cities was approximately 6 minutes slow for cycling to transit compared to driving, however, the distribution was wider for cycling to transit compared to driving. 

## References

* Yasmin, Farhana & Larsen, Jacob & El-Geneidy, Ahmed. (2010). Examining travel distances by walking and cycling, Montréal, Canada. https://www.researchgate.net/publication/258405294_Examining_travel_distances_by_walking_and_cycling_Montreal_Canada  Accessed February 13, 2024. 
* Larsen J., El-Geneidy A. Beyond the quarter mile: Re-examining travel distances by active transportation (2010) Canadian Journal of Urban Research, 19 (1 SUPPL.), pp. 70 - 88
