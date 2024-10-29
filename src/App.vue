<template>
  <h1>Приложение погоды</h1>
  <select @change="select_city($event)">
      <option value="56.50,60.35">Екатеринбург</option>
      <option value="55.4745,49.687">Казань</option>
      <option value="47.1426,39.4238">Ростов-на-Дону</option>
    </select>
  <p v-if="!weather_data">Загрузка ... </p>
  <div v-else>
    <p>Температура: {{weather_data.main.temp}}</p>
    <p>Влажность: {{weather_data.main.humidity}}</p>
    <p>Давление: {{weather_data.main.pressure}}</p>
    <p>Описание: {{weather_data.weather[0].description}}</p>
    
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return {
      weather_data:null
    }
  },
  mounted() {
    fetch("https://api.openweathermap.org/data/2.5/weather?lat=57.5500&lon=59.5800&appid=dc2d023e8e2bdb5838ca882823772060&units=metric&lang=ru")
    .then(resp=>resp.json())
    .then(json=> {
      this.weather_data=json;
    });
  },
  methods: {
    select_city(city) {
    fetch(`https://api.openweathermap.org/data/2.5/weather?lat=${city.target.value.split(",")[0]}&lon=${city.target.value.split(",")[1]}&appid=dc2d023e8e2bdb5838ca882823772060&units=metric&lang=ru`)
    .then(resp=>resp.json())
    .then(json=> {
      this.weather_data=json;
    });
  },
  components: {
  }
}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
