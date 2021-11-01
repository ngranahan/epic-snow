<template>
  <div class="app__body">
    <header class="header">
      <h1 class="header__title text-brand heading-primary">Epic Snow Report</h1>
    </header>
    <main class="main">
      <div class="container">
        <!-- Render form on load -->
        <QueryForm v-if="!results.length" :locationList="locationList" @formSubmit="getData"></QueryForm>
        <!-- Render dashboard on submit -->
        <!-- TODO: Results/Card Rendering -->
        <Card v-for="result in results" :key="result.data.nearest_area[0].areaName[0].value"></Card>
      </div>
    </main>
    <footer class="footer">
      <MountainsSVG></MountainsSVG>
      <div class="container">
        <nav class="footer__nav">
          <ul class="footer__nav-list">
            <li class="footer__nav-item"><a href="#" class="footer__nav-link text body-base">About</a></li>
            <li class="footer__nav-item"><a href="#" class="footer__nav-link text body-base">GitHub</a></li>
          </ul>
        </nav>
      </div>
    </footer>
    <!-- <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" /> -->
  </div>
</template>

<script>
import QueryForm from './components/QueryForm.vue';
import MountainsSVG from './components/MountainsSVG.vue';
import Card from './components/Card.vue';

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
        'allLocations',
        'northEast',
        'west',
        'midWest',
        'international'
      ],
      locationList: [
        {
          name: 'vail',
          label: 'Vail, CO',
          searchLocation: 'vail,co',
          region: 'west'
        },
        {
          name: 'whistler',
          label: 'Whistler Blackcomb, BC',
          searchLocation: 'whistler,bc',
          region: 'west'
        },
        {
          name: 'keystone',
          label: 'Keystone, CO',
          searchLocation: 'keystone,co',
          region: 'west'
        }
      ],
      results: []
    };
  },
  methods: {
    async getData(locationQuery) {
      console.log('getting data');
      const baseUrl = 'https://api.worldweatheronline.com/premium/v1/ski.ashx';
      const key = process.env.VUE_APP_API_KEY;
      try {
        for (const location of locationQuery) {
          const res = await fetch(`${baseUrl}?key=${key}&q=${location}&num_of_days=3&format=json&includeLocation=yes`);
          if (res.ok) {
            const data = await res.json();
            this.results.push(data);
            console.log('data', data);
          } else {
            // TODO: Handle error state in the UI
            throw new Error('Error fetching results.');
          }
        }
      } catch (e) {
        console.error(e);
      }
    },
    cacheData() {
      // TODO: Cache data
    }
  }
};
</script>
