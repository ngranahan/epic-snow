<template>
  <div class="app__body">
    <header class="header">
      <h1 class="header__title text-brand heading-primary"><a href="/">Epic Pass Snow Report</a></h1>
    </header>
    <main class="main">
      <div class="container container--spread">
        <!-- Render form on load -->
        <QueryForm
          v-if="!results.length"
          :locationList="locationList"
          :quickSearch="quickSearch"
          @formSubmit="getData"
        ></QueryForm>
        <!-- Render dashboard on submit -->
        <Card
          v-for="result in results"
          :key="result.location"
          :result="result"
        ></Card>
      </div>
      <p class="body-primary text-brand" v-if="error">{{ error }}</p>
    </main>
    <footer class="footer">
      <MountainsSVG></MountainsSVG>
      <div class="container">
        <nav class="footer__nav">
          <ul class="footer__nav-list">
            <li class="footer__nav-item"><a href="#" class="footer__nav-link text body-primary">About</a></li>
            <li class="footer__nav-item"><a href="https://github.com/ngranahan/epic-snow" class="footer__nav-link text body-primary">GitHub</a></li>
          </ul>
        </nav>
      </div>
    </footer>
  </div>
</template>

<script>
import QueryForm from './components/QueryForm.vue';
import MountainsSVG from './components/MountainsSVG.vue';
import Card from './components/Card.vue';
import locationList from './utils/locationList.js';

export default {
  name: 'App',
  components: {
    QueryForm,
    MountainsSVG,
    Card
  },
  data() {
    return {
      quickSearch: [
        {
          name: 'all',
          label: 'All US Mountains'
        },
        {
          name: 'midWest',
          label: 'Mid West Mountains'
        },
        {
          name: 'northEast',
          label: 'North East Mountains'
        },
        {
          name: 'west',
          label: 'West Coast Mountains'
        }
      ],
      locationList,
      results: [],
      error: ''
    };
  },
  methods: {
    async getData(locationQuery) {
      const baseUrl = 'https://api.worldweatheronline.com/premium/v1/ski.ashx';
      const key = process.env.VUE_APP_API_KEY;
      try {
        let queryArray;
        if (locationQuery.length === 1 && locationQuery[0] === 'all') {
          queryArray = this.locationList.map(location => location.searchLocation);
        } else if (locationQuery.length === 1 && this.quickSearch.filter(location => location.name === locationQuery[0]).length) {
          queryArray = this.locationList.filter(location => location.region === locationQuery[0]).map(location => location.searchLocation);
        } else {
          queryArray = locationQuery;
        }
        for (const location of queryArray) {
          const res = await fetch(`${baseUrl}?key=${key}&q=${location}&num_of_days=3&format=json&includeLocation=yes`);
          if (res.ok) {
            const data = await res.json();
            if (!data.data.error) {
              data.location = this.getLocationLabel(location);
              data.data.weather[0].totalSnowfall_in = this.formatSnowfall(data.data.weather[0].totalSnowfall_cm);
              this.results.push(data);
            } else {
              // No results for a given mountain. Return error message to the card component and log error in the console.
              data.location = this.getLocationLabel(location);
              data.vueError = 'Bummer! Looks like there\'s no snow report for this mountain.'
              this.results.push(data);
              console.error(data.data.error[0].msg);
            }
          } else {
            // No results for any mountains, render user friendly error message and log error.
            this.error = 'If you french fry when you\'re supposed to pizza, you\'re gonna have a bad time. No snow report right now. Check back l8r.'
            console.error('Error fetching results');
          }
        }
      } catch (e) {
        console.error(e);
      }
    },
    formatSnowfall(snowfallCM) {
      return (snowfallCM / 2.54).toFixed(2);
    },
    getLocationLabel(location) {
      const locationObj = this.locationList.find(item => { return item.searchLocation === location; });
      return locationObj.label;
    },
    cacheData() {
      // TODO: Cache data
    }
  }
};
</script>
