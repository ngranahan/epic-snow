<template>
  <form class="form" @submit.prevent="onSubmit">
    <h2 class="heading-secondary text-inverse">Quick Select</h2>
    <div class="form__group">
      <button
        @click="$emit('formSubmit', [button.name])"
        v-for="button in quickSearch"
        :key="button.name"
        class="button"
      >
        {{ button.label }}
      </button>
    </div>
    <h2 class="heading-secondary text-inverse">Select Mountains</h2>
    <div class="form__group">
      <!-- Checkboxes based on Sara Soueidan's method for accessible checkboxes: https://www.sarasoueidan.com/blog/inclusively-hiding-and-styling-checkboxes-and-radio-buttons/ -->
      <label
        v-for="checkbox in locationList"
        :key="checkbox.name"
        :for="checkbox.name"
        class="form__checkbox-label text-inverse body-primary"
      >
        <input
          type="checkbox"
          :id="checkbox.name"
          :value="checkbox.searchLocation"
          v-model="locationQuery"
          class="form__checkbox-input"
        />
        <!-- TODO: Maybe put this svg in another component for legibility -->
        <svg
          width="32"
          height="32"
          viewBox="-4 -4 39 39"
          aria-hidden="true"
          focusable="false"
          class="form__checkbox-svg"
        >
          <!-- The background -->
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
    </div>
    <button
      @click="$emit('formSubmit', locationQuery)"
      class="button"
      :class="[locationQuery.length ? activeClass : disabledClass]"
    >
      Get Snow Report
    </button>
  </form>
</template>

<script>
export default {
  name: 'QueryForm',
  props: ['locationList', 'quickSearch'],
  data() {
    return {
      locationQuery: [],
      activeClass: 'is-active',
      disabledClass: 'is-disabled',
      quickSelect: ''
    };
  }
};
</script>
