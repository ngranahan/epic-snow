<template>
  <div class="card">
    <div v-if="!result.vueError">
      <div
        v-for="(weather, index) in result.data.weather"
        :key="weather.date"
        class="card__content"
      >
        <div class="card__intro">
          <div class="card__text">
            <h2 v-if="index === 0" class="card__title heading-secondary text-brand">{{ result.location }}</h2>
            <p v-if="index === 0" class="card__subtitle body-tertiary text-brand">Today</p>
            <p v-else class="card__subtitle body-tertiary text-brand">{{ weather.date }}</p>
          </div>
          <div v-if="!result.vueError" class="card__intro-data">
            <p class="card__intro-data-figure heading-tertiary text-brand">{{ weather.chanceofsnow }}%</p>
            <p class="card__intro-data-text body-tertiary text-brand">Chance of Snow</p>
          </div>
        </div>
        <div class="card__body">
          <table class="card__table">
            <tr class="card__table-row">
              <th class="card__table-heading body-tertiary text-brand">Mountain Location</th>
              <th class="card__table-heading body-tertiary text-brand">High/Low Temp</th>
            </tr>
            <tr class="card__table-row">
              <td class="card__table-data body-secondary text-brand">Base</td>
              <td class="card__table-data body-secondary text-brand">{{ weather.bottom[0].maxtempF }}&deg;F / {{ weather.bottom[0].mintempF }}&deg;F</td>
            </tr>
            <tr class="card__table-row">
              <td class="card__table-data body-secondary text-brand">Middle</td>
              <td class="card__table-data body-secondary text-brand">{{ weather.mid[0].maxtempF }}&deg;F / {{ weather.mid[0].mintempF }}&deg;F</td>
            </tr>
            <tr class="card__table-row">
              <td class="card__table-data body-secondary text-brand">Top</td>
              <td class="card__table-data body-secondary text-brand">{{ weather.top[0].maxtempF }}&deg;F / {{ weather.top[0].mintempF }}&deg;F</td>
            </tr>
          </table>
          <p class="card__data heading-secondary text-brand">Total Snowfall: {{ weather.totalSnowfall_in }} in.</p>
        </div>
      </div>
    </div>
    <div v-else>
      <div class="card__intro">
        <div class="card__text">
          <h2 class="card__title heading-secondary text-brand">{{ result.location }}</h2>
          <p class="body-primary text-brand" >{{ result.vueError }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'card',
  props: ['result']
};
</script>
