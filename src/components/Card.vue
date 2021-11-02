<template>
  <div class="card">
    <div class="card__heading">
      <div class="card__text">
        <h2 class="card__title heading-secondary text-brand">{{ result.location }}</h2>
        <p class="card__subtitle body-tertiary text-brand">Today</p>
      </div>
      <div class="card__snowfall">
        <p class="card__snowfall-data heading-primary text-brand">{{ result.data.weather[0].chanceofsnow }}%</p>
        <p class="card__snowfall-detail body-tertiary text-brand">Chance of Snow</p>
      </div>
    </div>
    <table class="card__table">
      <tr class="card__table-row">
        <td class="card__table-data body-secondary text-brand">Base</td>
        <td class="card__table-data body-secondary text-brand">{{ result.data.weather[0].bottom[0].maxtempF }}/{{ result.data.weather[0].bottom[0].mintempF }}</td>
      </tr>
      <tr class="card__table-row">
        <td class="card__table-data body-secondary text-brand">Middle</td>
        <td class="card__table-data body-secondary text-brand">{{ result.data.weather[0].mid[0].maxtempF }}/{{ result.data.weather[0].mid[0].mintempF }}</td>
      </tr>
      <tr class="card__table-row">
        <td class="card__table-data body-secondary text-brand">Top</td>
        <td class="card__table-data body-secondary text-brand">{{ result.data.weather[0].top[0].maxtempF }}/{{ result.data.weather[0].top[0].mintempF }}</td>
      </tr>
    </table>
</div>
</template>

<script>
export default {
  name: 'card',
  props: ['result']
};
</script>
