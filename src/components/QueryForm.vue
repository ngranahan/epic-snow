<template>
  <form action="" class="form">
    <!-- Based on Sara Soueidan's method for accessible checkboxes: https://www.sarasoueidan.com/blog/inclusively-hiding-and-styling-checkboxes-and-radio-buttons/ -->
    <label
      v-for="checkbox in locationList"
      :key="checkbox.name"
      :for="checkbox.name"
      :class="{ 'is-checked': checkbox.checked }"
      class="form__checkbox-label text-inverse body-primary"
    >
      <input type="checkbox" :id="checkbox.name" class="form__checkbox-input" />
      <!-- TODO: Maybe put this svg in another component for legibility -->
      <!-- width="32"
      height="32" 
      viewBox="-4 -4 39 39" -->
      <svg
        width="32"
        height="32"
        viewBox="-4 -4 39 39"
        aria-hidden="true"
        focusable="false"
        class="form__checkbox-svg"
      >
        <!-- The background -->
        <!-- width="35"
          height="35" -->
        <rect
          class="form__checkbox-background"
          width="35"
          height="35"
          x="-2"
          y="-2"
          stroke="currentColor"
          fill="none"
          stroke-width="3"
          rx="6"
          ry="6"
        ></rect>
        <!-- The checkmark-->
        <polyline
          class="form__checkbox-checkmark"
          points="4,14 12,23 28,5"
          stroke="transparent"
          stroke-width="4"
          fill="none"
        ></polyline>
      </svg>
      <span class="form__label-text">{{ checkbox.label }}</span>
    </label>
  </form>
</template>

<script>
export default {
  name: 'QueryForm',
  props: ['locationList']
};
</script>
