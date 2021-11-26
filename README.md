# epic-snow

A simple vue dashboard app that renders the snow report for US mountain resorts on the Epic Pass.

# Mountain and Weather Data
Mountain names and locations are pulled from epicpass.com, via a serverless webscraper and custom REST API, which is maintained in a separate [repositiory](https://github.com/ngranahan/epic-resorts).

The mountain locations are used to retreive snow report data from the [World Weather Online Ski and Mountain Weather API](https://www.worldweatheronline.com/developer/api/docs/ski-weather-api.aspx), based on user input. While the ski weather API documentation indicates that 7 day ski weather forecast should be available, that feature doesn't seem to be working currently. The application has been structured in a way to render future weather forecast, based on the data structure outline in the API, though the results are currently only rendering the snow report for the current day.

An API key for the World Weather Online API needs to be defined in `.env.local` for local development.

# Data Caching
The app uses session storage to cache the resort lists after the initial call to the custom REST API. This enables users to execute multiple search queries in one browser session without having to wait for the resort list to populate each time.

# Hosting and Deployment
The app is deployed on Netlfy and can be accessed [here](https://epic-snow.netlify.app/).

# Development

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
