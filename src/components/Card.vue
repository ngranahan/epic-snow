<template>
  <div class="card">
    <div class="card__heading">
      <div class="card__text">
        <h2 class="card__title heading-secondary text-brand">{{ result.location }}</h2>
        <p class="card__subtitle body-tertiary text-brand">Today</p>
      </div>
      <div class="card__heading-data">
        <p class="card__heading-data-figure heading-primary text-brand">{{ result.data.weather[0].chanceofsnow }}%</p>
        <p class="card__heading-data-text body-tertiary text-brand">Chance of Snow</p>
      </div>
    </div>
    <table class="card__table">
      <tr class="card__table-row">
        <th class="card__table-heading body-tertiary text-brand">Mountain Location</th>
        <th class="card__table-heading body-tertiary text-brand">High/Low Temp</th>
      </tr>
      <tr class="card__table-row">
        <td class="card__table-data body-secondary text-brand">Base</td>
        <td class="card__table-data body-secondary text-brand">{{ result.data.weather[0].bottom[0].maxtempF }}&deg;F / {{ result.data.weather[0].bottom[0].mintempF }}&deg;F</td>
      </tr>
      <tr class="card__table-row">
        <td class="card__table-data body-secondary text-brand">Middle</td>
        <td class="card__table-data body-secondary text-brand">{{ result.data.weather[0].mid[0].maxtempF }}&deg;F / {{ result.data.weather[0].mid[0].mintempF }}&deg;F</td>
      </tr>
      <tr class="card__table-row">
        <td class="card__table-data body-secondary text-brand">Top</td>
        <td class="card__table-data body-secondary text-brand">{{ result.data.weather[0].top[0].maxtempF }}&deg;F / {{ result.data.weather[0].top[0].mintempF }}&deg;F</td>
      </tr>
    </table>
    <p class="card__data heading-secondary text-brand">Total Snowfall: {{ result.data.weather[0].totalSnowfall_in }} in.</p>
  </div>
</template>

<script>
export default {
  name: 'card',
  props: ['result']
};
</script>
