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

We have 5 main pages - Home, Timeline, Demographics, Impact and Events present as components - [HomeComponent.js](HomeComponent.js), TimelineComponent.js, DemographicsComponent.js, ImpactComponent.js and EventsComponent.js in src/components. We also have a MainComponent.js which carries the Main component which has the router for all these pages. The Main Component is called in App.js. 


