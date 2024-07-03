# Combining Mass Rapid Transit and Active Transportation for Physical Activity Promotion

## Objectives 

To compare travel distance and physical activity amounts attained from point-to-point travel by automobile to CBD station, bus to MRT to CBD station, and by AT to MRT to CBD station.

##  Scope of work

Using online tools such as Google maps travel planning or R5 (Rapid Realistic Routing on Real-world and Reimagined networks), this project will compare two MRT stations on the fringes of 6 major Canadian Cities: 

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


Routing tools will be used to compare travel time, travel distance, and estimated physical activity contribution of trips from 25 randomly selected street addresses within a 5km buffer of these two stations to the downtown central business districts (CBD). For each trip, the driving distance from the home street address to the CBD will be compared to a trip that is completed fully using public transit, and one that involves walking (if the MRT is less than 1km from the home) or biking (if the MRT is greater than 1km from the home but less than 5km) from the home. Below we provide an example with one street address (189 Portrush Ave, Ottawa, ON K2J 5K1) for the Fallowfield station BRT station in Ottawa to Downtown Ottawa. 

## Data and Code

The data and code are available for all stations. You will need the following to run the code

* GoogleMaps API Key 
    * Parameter is set as `map_key` in each file. You can register for a GoogleMaps API Key in the Google Developers portal.
* Required packages
    * googleway
    * tidyverse
    * ggmap
    * sf
    * sfext
    * googlePolylines
    * mapview
    * jsonlite
    * collapse

Each station as it's own R Markdown file that will need to edited if the code is be rerun. The following code blocks need to be edited at the beginning and end of the document. These blocks are labelled with an `EDIT ME` tag and the end of the code block.

#### Beginning of Document

* Draw buffer and select points 
    * The arrival destination
* Set origin point
    * The departure station
* Setup departure location and arrival time
    * The arrival time. Note the the date needs to be in the future and watch the time zone. 
* List of variables for geocoding
    * This is the list for parsing the JSON return from the GoogleMaps API. If a location does not geocode you will need to edit to the correct number. By default there should be 25 locations. 
* Seed
    * This sets the seed for the random generation of points within the generated buffer
    
#### End of Document

* Writing CSV Files
    * Provide file names and locations for the 2 datasets to be saved


City  | Station | Markdown | CSV Files
------------- | ------------- | ------------- | -------------
Ottawa  | Blair Station | [Click here](https://github.com/walkabilly/phac_routing/blob/main/Ottawa/Ottawa_Blaire_Station.md) | [Download](https://github.com/walkabilly/phac_routing/blob/main/Ottawa/ottawa_blaire_bike_transit_drive.csv)
Ottawa  | Barrhaven | [Click here](https://github.com/walkabilly/phac_routing/blob/main/Ottawa/Ottawa_Barrhaveb_Station.md) | [Download](https://github.com/walkabilly/phac_routing/blob/main/Ottawa/ottawa_barrhaven_bike_transit_drive.csv)
Montreal  | Brossard Station | [Click here](https://github.com/walkabilly/phac_routing/blob/main/Montreal/Montreal_Brossard_Station.md) | [Download](https://github.com/walkabilly/phac_routing/blob/main/Montreal/Montreal_Brossard_bike_transit_drive.csv)
Montreal  | Rivière-des-Prairies Station | [Click here](https://github.com/walkabilly/phac_routing/blob/main/Montreal/Montreal_RivierePrairie_Station.md) | [Download](https://github.com/walkabilly/phac_routing/blob/main/Montreal/montreal_riviereprairie_bike_transit_drive.csv)
Toronto  | Vaughan Metropolitan Centre Station | [Click here](https://github.com/walkabilly/phac_routing/blob/main/Toronto/Toronto_Vaughn_Station.md) | [Download](https://github.com/walkabilly/phac_routing/blob/main/Toronto/Toronto_Vaughn_bike_transit_drive.csv)
Toronto  | Scarborough GO Station | [Click here](https://github.com/walkabilly/phac_routing/blob/main/Toronto/Toronto_Scarborough_Station.md) | [Download](https://github.com/walkabilly/phac_routing/blob/main/Toronto/Toronto_Scarborough_bike_transit_drive.csv)
Edmonton  | Heritage Valley Station | [Click here](https://github.com/walkabilly/phac_routing/blob/main/Edmonton/Edmonton_Heritage_Station.md) | [Download](https://github.com/walkabilly/phac_routing/blob/main/Edmonton/edmonton_heritage_bike_transit_drive.csv)
Edmonton  | Nakî Transit Centre & Park and Ride | [Click here](https://github.com/walkabilly/phac_routing/blob/main/Edmonton/Edmonton_Naki_Station.md) | [Download](https://github.com/walkabilly/phac_routing/blob/main/Edmonton/Edmonton_Naki_bike_transit_drive.csv)
Calgary  | North Pointe Transit Terminal | [Click here](https://github.com/walkabilly/phac_routing/blob/main/Calgary/Calgary_NorthPoint_Station.md) | [Download](https://github.com/walkabilly/phac_routing/blob/main/Calgary/calgary_northpoint_bike_transit_drive.csv)
Calgary  | McKenzie Towne | [Click here](https://github.com/walkabilly/phac_routing/blob/main/Calgary/Calgary_McKenzie_Station.md) | [Download](https://github.com/walkabilly/phac_routing/blob/main/Calgary/calgary_mckenzie_bike_transit_drive.csv)
Vancouver  | Surrey Central Station | [Click here](https://github.com/walkabilly/phac_routing/blob/main/Vancouver/Vancouver_Surrey_Station.md) | [Download](https://raw.githubusercontent.com/walkabilly/phac_routing/main/Vancouver/vancouver_surrey_bike_transit_drive.csv)
Vancouver  | Bridgeport Station | [Click here](https://github.com/walkabilly/phac_routing/blob/main/Vancouver/Vancouver_Bridgeport_Station.md) | [Download](https://raw.githubusercontent.com/walkabilly/phac_routing/main/Vancouver/vancouver_bridgeport_bike_transit_drive.csv)

## Data Analysis

[Click to view Rendered Markdown](https://github.com/walkabilly/phac_routing/blob/main/data_analysis.md)


