<template>
  <div>
    <h2>Hourly Weather</h2>
    <div v-if="hourlyWeather">
      <div v-for="forecast in hourlyWeather" :key="forecast.dt" class="hourly-forecast">
        <div>{{ new Date(forecast.dt * 1000).toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' }) }}</div>
        <div>{{ Math.round(forecast.main.temp) }}°c</div>
        <div>{{ forecast.weather[0].main }}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HourlyWeather',
  props: {
    hourlyWeather: Array
  }
};
</script>

<style scoped>
/* Add your CSS styles here */
</style>
