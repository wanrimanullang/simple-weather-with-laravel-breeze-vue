<template>
  <div class="min-h-screen bg-gray-100 flex flex-col items-center justify-center">
    <div class="bg-white rounded-lg shadow-lg p-8 text-center">
      <h1 class="text-2xl font-bold mb-4">Weather App</h1>
      <img :src="weatherIconUrl" :alt="weatherDescription" class="mx-auto mb-4">
      <h2 class="text-xl font-semibold mb-2">{{ city }}</h2>
      <p class="text-gray-600">{{ weather }}</p>
      <div class="flex justify-center items-center mt-6">
        <div class="text-center">
          <p class="text-gray-600">Temperature</p>
          <p class="text-3xl font-bold">{{ temperature }}°C</p>
        </div>
        <div class="mx-6 border-r-2 border-gray-300"></div>
        <div class="text-center">
          <p class="text-gray-600">Humidity</p>
          <p class="text-3xl font-bold">{{ humidity }}%</p>
        </div>
        <div class="mx-6 border-r-2 border-gray-300"></div>
        <div class="text-center">
          <p class="text-gray-600">Wind Speed</p>
          <p class="text-3xl font-bold">{{ windSpeed }} km/h</p>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import axios from 'axios'
export default {
  props: ['city'],
  data() {
    return {
      location: '',
      lastUpdated: '',
      temperature: null,
      weatherDescription: '',
      weatherIconUrl: '',
      humidity: null,
      windSpeed: null
    }
  },
  mounted() {
    this.getWeatherData();
  },
  methods: {
    async getWeatherData() {
      try {
        const response = await axios.get(`http://api.weatherstack.com/current?access_key=6903b3cb38b393b0edcdfe5de3a5e133&query=Jakarta`);
        const data = response.data;
        console.log(data);
        this.location = data.location.name;
        this.lastUpdated = data.current.observation_time;
        this.temperature = data.current.temperature;
        this.weatherDescription = data.current.weather_descriptions[0];
        this.weatherIconUrl = data.current.weather_icons[0];
        this.humidity = data.current.humidity;
        this.windSpeed = data.current.wind_speed;
      } catch (error) {
        console.log(error);
      }
    }
  }
}
</script>