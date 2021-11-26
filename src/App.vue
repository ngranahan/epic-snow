<template>
  <div class="app__body">
    <header class="header">
      <h1 class="header__title text-brand heading-primary"><a href="/">Epic Pass Snow Report</a></h1>
    </header>
    <main class="main">
      <transition name="main-fade">
        <div v-if="locationList.length">
          <div class="container container--spread">
            <QueryForm
              v-if="!results.length"
              :locationList="locationList"
              :quickSearch="quickSearch"
              @formSubmit="getData"
            ></QueryForm>
            <Card
              v-for="result in results"
              :key="result.location"
              :result="result"
            ></Card>
          </div>
        </div>
        <div v-else>
          <Loading />
        </div>
      </transition>
      <p class="body-primary text-brand" v-if="error">{{ error }}</p>
    </main>
    <Footer></Footer>
  </div>
</template>

<script>
import QueryForm from './components/QueryForm.vue';
import Footer from './components/Footer.vue';
import Card from './components/Card.vue';
import Loading from '@/components/Loading.vue';

export default {
  name: 'App',
  components: {
    QueryForm,
    Footer,
    Card,
    Loading
  },
  data() {
    return {
      quickSearch: [],
      locationList: [],
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
          queryArray = this.locationList.map(location => `${location.location.lat},${location.location.lng}`);
        } else if (locationQuery.length === 1 && this.quickSearch.filter(location => location.name === locationQuery[0]).length) {
          queryArray = this.locationList.filter(location => location.region === locationQuery[0]).map(location => `${location.location.lat},${location.location.lng}`);
        } else {
          queryArray = locationQuery;
        }
        for (const location of queryArray) {
          const res = await fetch(`${baseUrl}?key=${key}&q=${location}&num_of_days=3&format=json&includeLocation=yes`);
          if (res.ok) {
            const data = await res.json();
            if (!data.data.error) {
              data.location = this.getLocationLabel(location);
              data.data.weather.forEach(item => {
                item.totalSnowfall_in = this.formatSnowfall(item.totalSnowfall_cm);
                item.date = this.formatDate(item.date);
              });
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
    formatDate(date) {
      const isoDate = new Date(date);
      let str = isoDate.toDateString();
      const firstIndex = str.indexOf(' ');
      str = str.slice(firstIndex + 1);
      return str;
    },
    formatSnowfall(snowfallCM) {
      return (snowfallCM / 2.54).toFixed(2);
    },
    getLocationLabel(location) {
      const lat = parseFloat(location.split(',')[0]);
      const lng = parseFloat(location.split(',')[1]);
      const locationObj = this.locationList.find(item => { return item.location.lat === lat && item.location.lng === lng; });
      return locationObj.label;
    },
    formatLabel(text) {
      const words = text.match(/[A-Za-z][a-z]*/g) || [];
      const capitalized = words.map(word => {return word.charAt(0).toUpperCase() + word.substring(1)});
      return capitalized.length > 1 ? capitalized.join('-') : capitalized[0];
    }
  },
  async mounted() {
    const res = await fetch(`https://b2y7xrww3j.execute-api.us-east-1.amazonaws.com/production/resorts`);
    if (res.ok) {
      const data = await res.json();
      const quickSearch = [
        {
          name: 'all',
          label: 'All Mountains'
        }
      ];
      Object.keys(data.regions).forEach(region => {
        const regionObj = {
          name: region,
          label: this.formatLabel(region)
        }
        quickSearch.push(regionObj)
      })
      this.quickSearch = quickSearch;
      this.locationList = data.resorts;
    }
  }
};
</script>
