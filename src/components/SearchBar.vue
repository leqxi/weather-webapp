<template>
  <div class="search-box">
    <input 
      type="text" 
      class="search-bar" 
      placeholder="Search..."
      v-model="query"
      @keypress.enter="fetchWeather"
    />
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  data() {
    return {
      query: ''
    };
  },
  methods: {
    fetchWeather() {
      this.$emit('search', this.query);
    }
  }
};
</script>

<style scoped>
/* Add your CSS styles here */
</style>
