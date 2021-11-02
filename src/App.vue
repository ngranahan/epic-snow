<template>
  <div class="app__body">
    <header class="header">
      <h1 class="header__title text-brand heading-primary">Epic Pass Snow Report</h1>
    </header>
    <main class="main">
      <div class="container">
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
    </main>
    <footer class="footer">
      <MountainsSVG></MountainsSVG>
      <div class="container">
        <nav class="footer__nav">
          <ul class="footer__nav-list">
            <li class="footer__nav-item"><a href="#" class="footer__nav-link text body-base">About</a></li>
            <li class="footer__nav-item"><a href="https://github.com/ngranahan/epic-snow" class="footer__nav-link text body-base">GitHub</a></li>
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
      results: []
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
            if (!data.error) {
              data.location = this.getLocationLabel(location);
              this.results.push(data);
            } else {
              // TODO: Handle error state in the UI
              // No results for a specific location. Probably still want to load a card for that mountain but just include a message about no snow report
              throw new Error(data.error);
            }
          } else {
            // TODO: Handle error state in the UI
            // No results, render error message in search form
            throw new Error('Error fetching results.');
          }
        }
      } catch (e) {
        console.error(e);
      }
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
