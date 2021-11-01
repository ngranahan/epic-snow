<template>
  <form action="" class="form">
    <!-- Checkboxes -->
    <div class="form__group" v-for="location in locationList" :key="location.name">
      <input type="checkbox" :id="location.name" v-model="checked" class="form__input" />
      <label :for="location.name" class="form__label">{{ location.label }}</label>
    </div>
  </form>
</template>

<script>
export default {
  name: 'QueryForm',
  props: ['locationList'],
  data() {
    return {
      checked: []
    };
  }
};
</script>
