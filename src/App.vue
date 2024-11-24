
<template>
  <h1>Приложение погоды</h1>
  <select @change="city($event)" class="bat">
    <option value="57.9194/59.965">Нижний Тагил</option>
    <option value="55.7522/37.6156">Москва</option>
    <option value="55.7887/49.1221">Казань</option>
  </select>
  <p v-if="!weather_date">Загрузка ...</p>

  <div v-else class="bod">
    <div v-if="forecast_date">
      <ForecastCar v-for="(f, i) in forecast_date.list" :key="i" :weather_date="f"></ForecastCar>
    </div>
  </div>

</template>

<script>
import ForecastCar from './components/ForecastCar.vue';

export default {
  name: 'App',
  data() {
    return {
      weather_date: null,
      forecast_date: null
    }
  },
  mounted() {
    //fetch("https://api.openweathermap.org/data/2.5/weather?lat=57.9194&lon=59.965&appid=5aabb0813a2a69e1ca65a89ecae8e3fd&lang=ru&units=metric")
      fetch('weather.json')
      .then(resp => resp.json())
      .then(json => {
        this.weather_date = json;
      })
    //fetch("https://api.openweathermap.org/data/2.5/forecast?lat=57.9194&lon=59.965&appid=5aabb0813a2a69e1ca65a89ecae8e3fd&lang=ru&units=metric")
      fetch('forecast.json')
      .then(resp => resp.json())
      .then(json => {
        this.forecast_date = json;
      })
  },
  methods: {
    city(sity) {
      fetch(`https://api.openweathermap.org/data/2.5/weather?lat=${sity.target.value.split("/")[0]}&lon=${sity.target.value.split("/")[1]}&appid=5aabb0813a2a69e1ca65a89ecae8e3fd&lang=ru&units=metric`)
        .then(resp => resp.json())
        .then(json => {
          this.weather_date = json;
        });
      fetch(`https://api.openweathermap.org/data/2.5/forecast?lat=${sity.target.value.split("/")[0]}&lon=${sity.target.value.split("/")[1]}&appid=5aabb0813a2a69e1ca65a89ecae8e3fd&lang=ru&units=metric`)
        .then(resp => resp.json())
        .then(json => {
          this.forecast_date = json;
        });
    }
  },
  components: {
    ForecastCar
  }
}
</script>

<style>
#app {

  text-align: center;
}
h1 {
    color: rgb(165, 62, 168);
  }
body {
  background-color: rgb(231, 217, 226);
  font-family: Arial;
}

</style>
