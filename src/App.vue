<template>
  <header class="header">
    <h1 class="header__title text-brand heading-primary">Epic Snow Report</h1>
  </header>
  <main class="main">
    <div class="container">
      <!-- Render form on load -->
      <QueryForm :locationList="locationList"></QueryForm>
      <!-- Render dashboard on submit -->
      <Card></Card>
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
          location: 'vail, co',
          region: 'west'
        },
        {
          name: 'whistler',
          label: 'Whistler Blackcomb, BC',
          location: '',
          region: 'west'
        },
        {
          name: 'keystone',
          label: 'Keystone, CO',
          location: '',
          region: 'west'
        }
      ]
    };
  }
};
</script>
