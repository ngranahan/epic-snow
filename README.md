# epic-snow

A simple vue dashboard app that renders the snow report for US mountain resorts on the Epic Pass.

# Mountain and Weather Data

Mountain names and locations are stored in `src/utils/locationList.js` and used to call the [World Weather Online Ski Weather API](https://www.worldweatheronline.com/developer/api/docs/ski-weather-api.aspx) based on user input.

While the API documentation indicates that 7 day ski weather forecast should be available, that feature doesn't seem to be working currently. The application has been structured in a way to render future weather forecast, based on the data structure outline in the API, though the results are currently only rendering the snow report for the current day.

An API key needs to be defined in `.env.local` for local development.

# Hosting and Deployment
The app is deployed on Netlfy and can be accessed [here](https://epic-snow.netlify.app/).

# Considerations and Enhancements

## Data Caching
The first enhancement that I'd likely do would be to cache the weather data so that the app isn't making unnecessry API calls. The API documentation indicates that weather is reported every 24 hours so caching weather data for a day would make the most sense. This would help to make sure that the app doesn't run into issues with rate limits or performance issues if more data is getting returned. The API calls are returning data quickly now but they may start to lag if the API starts returning future weather forecasts.

The Vue documentation recommends using local storage for client side caching so that's likely where I would start for this enhancement but this could be a lot of data for local storage so it may be worth exploring other options.

## Dynamically Loading Mountain Data
Ideally the app would load in the Epic Pass Mountains dynamically so that the app could stay up to date season to season as the participating mountains change. In order to do this, I considered scraping the location data from the Epic Pass website, which has a well strutured list of the mountain resorts, but decided not to move forward with that approach at this time since that would also require geocoding the locations and felt unnecessary at this time. If I end up using this app frequently this ski season I would definitely circle back to this feature.

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
