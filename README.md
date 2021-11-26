# epic-snow

A simple vue dashboard app that renders the snow report for US mountain resorts on the Epic Pass.

# Mountain and Weather Data
Mountain names and locations are pulled from epicpass.com, via a serverless webscraper and custom REST API, which is maintained in a separate [repositiory](https://github.com/ngranahan/epic-resorts).

The mountain locations are used to retreive snow report data from the [World Weather Online Ski and Mountain Weather API](https://www.worldweatheronline.com/developer/api/docs/ski-weather-api.aspx), based on user input. While the ski weather API documentation indicates that 7 day ski weather forecast should be available, that feature doesn't seem to be working currently. The application has been structured in a way to render future weather forecast, based on the data structure outline in the API, though the results are currently only rendering the snow report for the current day.

An API key for the World Weather Online API needs to be defined in `.env.local` for local development.

# Hosting and Deployment
The app is deployed on Netlfy and can be accessed [here](https://epic-snow.netlify.app/).

# Considerations and Enhancements

## Data Caching
The first enhancement that I'd likely do would be to cache the resort data so that the app loads faster after the initial page load. 

Cashing the weather data would also be a good idea to avoide unnecessary calls to the ski weather API. The API documentation indicates that weather is reported every 24 hours so caching weather data for a day would make the most sense. This would help to make sure that the app doesn't run into issues with rate limits or performance issues if more data is getting returned. The API calls are returning data quickly now but they may start to lag if the API starts returning future weather forecasts.

The Vue documentation recommends using local storage for client side caching so that's likely where I would start for this enhancement but this could be a lot of data for local storage so it may be worth exploring other options.

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
