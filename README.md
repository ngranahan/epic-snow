# epic-snow

A simple vue dashboard app that renders the snow report for US mountain resorts on the Epic Pass.

# Mountain and Weather Data

Mountain names and locations are stored in `src/utils/locationList.js` and used to call the [World Weather Online Ski Weather API](https://www.worldweatheronline.com/developer/api/docs/ski-weather-api.aspx) based on user input.

While the API documentation indicates that 7 day ski weather forecast should be available, that feature doesn't seem to be working currently. The application has been structured in a way to render future weather forecast, based on the data structure outline in the API, though the results are currently only rendering the snow report for the current day.

An API key needs to be defined in `.env.local` for local development.

# Hosting and Deployment
The app is deployed on Netlfy and can be accessed [here](https://epic-snow.netlify.app/).

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```
