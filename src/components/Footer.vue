<template>
  <footer class="footer">
    <MountainsSVG></MountainsSVG>
    <div class="footer__body">
      <div class="container">
        <transition name="about-slide-fade">
          <About v-if="showAbout"></About>
        </transition>
        <nav class="footer__nav">
          <ul class="footer__nav-list">
            <li class="footer__nav-item"><a href="#" @click.prevent="toggleAbout" class="footer__nav-link text body-primary">About</a></li>
            <li class="footer__nav-item"><a href="https://github.com/ngranahan/epic-snow" class="footer__nav-link text body-primary">GitHub</a></li>
          </ul>
        </nav>
      </div>
    </div>
  </footer>
</template>

<script>
import MountainsSVG from './MountainsSVG.vue';
import About from './About.vue';

export default {
  name: 'Footer',
  components: {
    MountainsSVG,
    About
  },
  data() {
    return {
      showAbout: false
    };
  },
  methods: {
    toggleAbout() {
      this.showAbout = this.showAbout === false ? true : false;
    }
  }
};
</script>
