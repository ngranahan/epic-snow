<template>
  <div class="about" data-about>
    <p class="body-primary text">This simple vue app is designed to render the snow report for full-access mountain resorts on the 2021-2022 Epic Pass. The app pulls resort locations from a custom REST API, which scrapes resorts from the Epic Pass website. The resort locations (latitude and longitude) are then used to call the World Weather Online Ski Weather API, which returns chance of snow, total snowfall predicted, and temperature for base, mid, and summit sections of the mountain.</p>
  </div>
</template>

<script>
export default {
  name: 'About',
  mounted() {
    const bottom = document.querySelector('[data-about]');
    console.log('showAbout false', bottom);
    bottom.scrollIntoView(true);
  }
};
</script>
