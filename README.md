# Live Flight Tracker - Deployed to [https://uci-cubesat-live-tracker.herokuapp.com/](https://uci-cubesat-live-tracker.herokuapp.com/)

![[Website Status](https://uci-cubesat-live-tracker.herokuapp.com)](https://img.shields.io/website?down_color=lighgrey&down_message=offline&up_color=blue&up_message=online&url=https%3A%2F%2Fuci-cubesat-live-tracker.herokuapp.com%2F)

[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

## TODOs: Adding an additional `Satellite Layer` inside `react-map-gl`
This will require a new API endpoints in the backend server

`https://uci-cubesat-server.herokuapp.com/api/v1/satellite_state/{name}`

that return the current state of a satellite

Example of `curl 
https://uci-cubesat-server.herokuapp.com/api/v1/satellite_state?name=amicalsat`

Should return something like this:

```
{
  norad_cat_id: 41168
  sat_id: "VTHG-6292-4004-9767-5017"
  tle0: "ATHENOXAT 1",
  tle1: "1 41168U 15077C   22065.83439863  .00010033  00000+0  44232-3 0  9993",
  tle2: "2 41168  14.9916 129.3584 0009660 235.7803 270.3843 15.18062654344672",
  latLng: {
    lat: -77.88052870998666,
    lng: 36.95977766102887
  }
}
```

optionally, two additional api endpoints that describe the `route` and `satellite` can also be helpful

and a new `.src/services/cubesatAPIService.ts` `Service` module in the model similar to [openSkyAPIService.ts](https://github.com/UCI-CubeSat/UCI-CubeSat-Live-Tracker/blob/main/src/services/openSkyAPIService.ts)

and a new `./src/components/SatelliteLayer.tsx` `Satellite Layer` react component similar to [AircraftLayer.tsx](https://github.com/UCI-CubeSat/UCI-CubeSat-Live-Tracker/blob/main/src/components/AircraftLayer.tsx)

add a new `./src/cubesat` directory that has 
1. `constants.ts` which holds varies constants including the api endpoints URL
2. `index.ts` for exporting function/module
3. `types.ts` that describes the expected JSON payload from the backend api response

Satellite Flights are display and updated using a `subscription` model

`./src/components/SatelliteLayer.tsx` subscribe to active flights within map bounds, 
add them to a local register and listen for `status` change

`./src/cubesat/types.ts` and `./src/services/cubesatAPIService.ts` perform
the asynchronous fetch operation to get flight status response from the backend server

`./src/services/geospatialService.ts` perform additional calculation to prediction upcoming path change

## Description

Written with `React` and `TypeScript`.

The goal of this project is to read the data from [SatNogs Open Network](https://satnogs.org/) and [OpenSky Network](https://opensky-network.org/) and visualize it on a map.

![Preview GIF](docs/react-flight-tracker_prview.gif)

## 📦 Packages:
- [TypeScript](https://github.com/microsoft/TypeScript)
- [react-router](https://github.com/ReactTraining/react-router)
- [MUI](https://github.com/mui-org)
- [react-map-gl](https://github.com/visgl/react-map-gl)

## 🔮 Features:
- Using "Hooks", "Context", "Suspense", "React.lazy" and other popular React patterns.
- Written entirely in TypeScript.
- Using maps from [mapbox](https://www.mapbox.com/) with the React friendly wrapper [react-map-gl](https://github.com/visgl/react-map-gl).
- Using styling components from [MUI](https://github.com/mui-org) project.
- Fetching flight data from [OpenSky Network](https://opensky-network.org/).

## 🔌 Usage:
To use the maps from [mapbox](https://www.mapbox.com/), you need an appropriate token. You can create one on their website by registering there. Registration is free and all relevant things are covered for development purposes.

For the use of the flight data via [OpenSky Network](https://opensky-network.org/), I would also recommend creating a corresponding account on their website. The flight data is then provided with a delay of ~5 seconds. Without an account, the delay is ~10 seconds.

Start by cloning the repository and install the packages:
```
npm install
```
Create a `.env.local` file in the root directory containing following entries:
```
REACT_APP_MAPBOX_TOKEN=<YOUR_MAPBOX_TOKEN>
REACT_APP_OSKY_USERNAME=<YOUR_OPENSKYNETWORK_USERNAME>
REACT_APP_OSKY_PASSWORD=<YOUR_OPENSKYNETWORK_PASSWORD>
```
Start the project:
```
npm start
```

Build the project locally:
```
npm run build
serve -s build
```

Generating flight:

[https://opensky-network.org/api/states/all?&icao24=a535be](https://opensky-network.org/api/states/all?&icao24=a535be)

[https://opensky-network.org/api/routes?callsign=DAL283](https://opensky-network.org/api/routes?callsign=DAL283)

Deploying to Heroku:
[https://dashboard.heroku.com/apps/uci-cubesat-live-tracker](https://dashboard.heroku.com/apps/uci-cubesat-live-tracker)
