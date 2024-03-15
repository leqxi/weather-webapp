<template>
  <div id="app" class="app">
    <main>
      <div class="search-container">
        <SearchBar @search="fetchWeather" />
      </div>
      <div class="weather-container">
        <WeatherDisplay :weather="weather" />
      </div>
      <div class="hourly-weather">
          <HourlyWeather :hourlyWeather="hourlyWeather" />
      </div>
    </main>
  </div>
</template>

<script>
import SearchBar from './components/SearchBar.vue';
import WeatherDisplay from './components/WeatherDisplay.vue';
import HourlyWeather from './components/HourlyWeather.vue';

export default {
  name: 'app',
  components: {
    SearchBar,
    WeatherDisplay,
    HourlyWeather
  },
  data() {
    return {
      api_key: 'fe8acfdd54758055aa4f71011569f278',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      weather: null
    };
  },
  methods: {
    async fetchWeather(query) {
      try {
        const response = await fetch(`${this.url_base}weather?q=${query}&units=metric&APPID=${this.api_key}`);
        if (!response.ok) {
          throw new Error('City not found');
        }
        const data = await response.json();
        this.weather = data;
        
        const hourlyResponse = await fetch(`${this.url_base}forecast?q=${query}&units=metric&APPID=${this.api_key}`);
        if (!hourlyResponse.ok) {
          throw new Error('Failed to fetch hourly forecast');
        }
        const hourlyData = await hourlyResponse.json();
        this.hourlyWeather = hourlyData.list.filter((item, index) => index % 8 === 0);
      } catch (error) {
        console.error(error);
      }
    }
  }
};
</script>



<style scoped>
..app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

main {
  text-align: center;
}

.search-container {
  position: absolute;
  top: 20px;
  right: 20px;
}

.weather-container {
  margin-top: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
}
</style>
