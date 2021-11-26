<template>
  <div class="loading" data-loading></div>
</template>

<script>
export default {
  name: 'Loading',
  methods: {
    generateSnow() {
      const loadingComponent = document.querySelector('[data-loading]');
      for (let i = 0; i < 50; i++) {
        const div = document.createElement('div');
        div.className = 'loading__snowflake';
        loadingComponent.appendChild(div);
      }
    }
  },
  mounted() {
    this.generateSnow();
  }
};
</script>
