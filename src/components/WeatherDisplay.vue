<template>
  <div class="weather-wrap" v-if="weather">
    <div class="location-box">
      <div class="location">{{ weather.name }}</div>
    </div>

    <div class="weather-box">
      <div class="temp">{{ Math.round(weather.main.temp) }}°</div>
      <div class="weather">{{ weather.weather[0].main }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'WeatherDisplay',
  props: {
    weather: Object
  }
};
</script>

<style scoped>
.temp {
    font-size: 250%;
}
</style>
