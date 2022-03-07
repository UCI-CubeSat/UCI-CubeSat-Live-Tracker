# Live Flight Tracker
## Deployed to: [https://uci-cubesat-live-tracker.herokuapp.com/](https://uci-cubesat-live-tracker.herokuapp.com/)

## TODOs: Adding an additional `Satellite Layer` inside `react-map-gl`
This will require a new API endpoint in the backend server

`https://uci-cubesat-server.herokuapp.com/api/v1/satellite/{name}`

that return the current state of a satellite

```
{
  latLng: {
    lat: -77.88052870998666,
    lng: 36.95977766102887
  },
  latPath: [
    -77.88052870998666,
    ...,
    -80.35845117082839
  ],
  lngPath: [
    36.95977766102887,
    ...,
    24.027332976062507
  ]
}
```

and a new `Service` module in the model similiar to [openSkyAPIService.ts](https://github.com/UCI-CubeSat/UCI-CubeSat-Live-Tracker/blob/main/src/services/openSkyAPIService.ts)

and a new `Satellite Layer` react component similar to [AircraftLayer.tsx](https://github.com/UCI-CubeSat/UCI-CubeSat-Live-Tracker/blob/main/src/components/AircraftLayer.tsx)

## Description

Written with `React` and `TypeScript`.

The goal of this project is to read the data from [OpenSky Network](https://opensky-network.org/) and visualize it on a map.

[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

![](docs/react-flight-tracker_prview.gif)

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
