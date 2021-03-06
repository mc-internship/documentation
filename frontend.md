# Covid19Visualizer

A new perspective of visualization for Covid-19. 

## A Brief Description of The Project

This project involves developing a web dashboard for tracking the spread of Covid-19 in the five countries of 
India, USA, Germany, Italy and Singapore as well as providing important insights regarding the same. Trends, industry
impact, breakout of spread across demographics as well as government policies and their effect has been analysed in 
detail and shown in different sections of the website. This project was a part of the 4 week MasterCard internship carried
out in May 2020. This is a documentation focussing on the frontend side of the website. 

## Installation Instructions 

To run the website on your local server, do the following:

1. Clone the repository 
`git clone https://github.com/mc-internship/covid19visualizer.git`
2. Navigate to the frontend folder
3. Either run `bash entrypoint.sh` or `yarn install && yarn start`

## A Short Walkthrough 

The website has been hosted at the following link: [http://covid19visual.herokuapp.com/home](http://covid19visual.herokuapp.com/home). 

A short walkthrough of the various features of the website can be found [here](https://photos.app.goo.gl/xEL4B8GYS9kgBcTM9).

## Directory Structure 

The frontend has the following directory structure:
```-/|/'
   |-build
   |-public
   |---maps
   |-src
   |---components
   |-----ChartHelpers
   |-----DemographicsElements
   |-----ImpactElements
   |-----Mapscountry
   |-----TrendCharts
   |—shared

```
## Architecture and How Things Work

We have 5 main pages - Home, Timeline, Demographics, Impact and Events present as components [HomeComponent.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/components/HomeComponent.js), [TimelineComponent.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/components/TimelineComponent.js), [DemographicsComponent.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/components/DemographicsComponent.js), [ImpactComponent.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/components/ImpactComponent.js) and [EventsComponent.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/components/EventComponent.js) in src/components. We also have a [MainComponent.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/components/MainComponent.js) which carries the Main component which has the router for all these pages. The Main component is finally called in [App.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/App.js). 

### Helpers 
1. In src/components, we have a [dataexport.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/components/dataexport.js) file which fetches data from json files stored in a github repository. This data can be imported wherever required. This was done to reduce the time it takes to load a page, specially the district tables significantly. 
2. We have a [constants.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/constants.js) file in src which contains all the constants used across the files like state codes and exports the maps required for the country view.
3. [UtilFunctions.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/shared/UtilFunctions.js) in src/shared contains some utility functions used across the files like getting the state name from the state code and formatting numbers in the format we want.
4. [ChartHelpers](https://github.com/mc-internship/covid19visualizer/tree/master/frontend/src/components/ChartHelpers) - this folder in src/components contains the code for all the charts we’re using on the website like in the Timeline, Demographics and Impact section. All these charts use the React wrapper for Charts.js 2. 
5. [MapsCountry](https://github.com/mc-internship/covid19visualizer/tree/master/frontend/src/components/Mapscountry) - this folder in src/components contains the code for the maps and the tables which are displayed in the country view of a country. D3 library has primarily been used for visualisation of data. The main files are the following - 
   * [CholoplethComponent.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/components/Mapscountry/ChoroplethComponent.js) - This includes the code for the major map functionalities like setting size of the map, setting the color scale for the map, adding id to states and districts, highlighting regions on the map and how the map would behave on actions like on click, on hovering and after a region is selected. This also incorporates the legend from [Legend.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/components/Mapscountry/Legend.js). This is finally exported to [MapMain.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/components/Mapscountry/MapMain.js).
   * [RowComponent.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/components/Mapscountry/RowComponent.js) - This constructs the rows in the table for states and districts and connects the states and the districts in the table to those in the map, on highlighting or clicking. This also includes functions for sorting the table according to the most or least cases and alphabetically according to state/district names. All this is finally exported to [TableComponent.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/components/Mapscountry/TableComponent.js).
   * [StateStats.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/components/Mapscountry/StateStats.js) - This contains the function to display the stats of the state/district on the side of the map when we are hovering over those regions on the map.
   * [HeadBarAbove.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/components/Mapscountry/HeadBarAbove.js) - This contains the function to change the heatmap according to the four options of confirmed, active, recovered, and deceased. These are present as buttons below the maps.
   * [MainView.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/components/Mapscountry/MainView.js) - This is the main file for the country page. This takes the map component, table component, and the stats component as well the buttons to shift between different heatmaps, places them in separate div containers and exports them all to a country’s page. 

### Home 

The Home component in [HomeComponent.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/components/HomeComponent.js) consists of three elements - 
1. A news feed on the left which fetches data from a news api imported as news from [dataexport.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/components/dataexport.js). 
2. A rotating globe in the center  which is imported from [GlobeComponent.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/components/GlobeComponent.js). This uses the react-globe library. The globe is automatically rotating but it can also be pressed and dragged to take us to the country of our choice. The globe has 5 markers for the 5 countries we are considering. Clicking on these markers takes us to the country’s page. 
3. Five country cards on the right displaying the country’s stats like confirmed, active, recovered and deceased. Clicking on these cards also takes us to the country’s page. 

<img src="assets/Home.png" width="960" height="600" align="center" />

### Country’s Page

The country’s page displays the country map in the middle, table on the right and region stats on the left. Hovering on any region on the map highlights the region in the table and vice-versa and we also get the region stats on the left. To get the country stats, we click anywhere outside the map. These maps and tables are connected by a unique identifier which we are using as the state name/district name. For the map to function, in the topojsons we are using, we should have a field called “st_nm” for every region and this should exactly match the name we are using for the region in the database. 

The country pages like [IndiaComponent.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/components/IndiaComponent.js) import the code from [MainView.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/components/Mapscountry/MainView.js) for each country. 

<img src="assets/Country.png" width="960" height="600" align="center" />

### Timeline, Demographics, and Impact

These pages contain graphs for the 5 different countries displaying the trends, the demographics, and the main industries which have been impacted. These country files are present in the folders [TrendCharts](https://github.com/mc-internship/covid19visualizer/tree/master/frontend/src/components/TrendCharts), [DemographicsElements](https://github.com/mc-internship/covid19visualizer/tree/master/frontend/src/components/DemographicsElements) and [ImpactElements](https://github.com/mc-internship/covid19visualizer/tree/master/frontend/src/components/ImpactElements) respectively. We can navigate to the different countries using the side navigation bar. All the graphs used can be found in the [ChartHelpers](https://github.com/mc-internship/covid19visualizer/tree/master/frontend/src/components/ChartHelpers) folder. 

<img src="assets/Timeline.png" width="960" height="600" align="center" />

### Events Page

Events page displays two things for a country. First thing is the daily confirmed cases chart for a country which comes from the [ChartHelpers](https://github.com/mc-internship/covid19visualizer/tree/master/frontend/src/components/ChartHelpers) folder. Second is the list of events and government policy decisions that took place in a country. This is so that we can study how the events affected the total confirmed cases and if they were effective. This list is imported from [EventHelperComponent.js](https://github.com/mc-internship/covid19visualizer/blob/master/frontend/src/components/EventHelperComponent.js).

<img src="assets/Events.png" width="960" height="600" align="center" />

## Further Additions We Can Make

These things would make the existing website better, but couldn’t be done in the period of the internship because of lack of time - 

1. Incorporating elements of responsive design and making the website mobile-friendly and view-friendly
2. Adding maps for districts. This requires us to obtain the state topojsons which show districts and ensuring the the district names in the topojson and the database exactly match as well as it isn’t the case that one thing is present in the data but not in the topojson and vice-versa. This also includes adding the “st_nm” and “id” field in the topojsons, if not already present
3. Adding a time slider to the globe as well as to all the country maps which shows how the cases spread with time and what path of spread they followed 





