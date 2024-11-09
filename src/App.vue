<template>
  <h1>Приложение погоды Api-Weather</h1>
  <select @change="city($event)">
   <option value="56.50,60.35">Екатеринбург</option>
   <option value="55.4745,49.687">Казань</option>
   <option value="47.1426,39.4238">Ростов-на-Дону</option>
   </select>
  <p v-if="!weather_data">Загрузка ...</p>
  <div v-else>
   <h2>{{ weather_data.city.name }} </h2>
   <table>
    <tr><td>
     <p class="day">Первый день:</p>
     <p>Температура:{{ weather_data.list[0].main.temp }}</p>
     <p>Влажность:{{ weather_data.list[0].main.humidity }}</p>
     <p>Давление:{{ weather_data.list[0].main.pressure }}</p>
     <p>Описание:{{ weather_data.list[0].weather[0].description }}</p>
     <img 
  :src="`https://openweathermap.org/img/wn/${weather_data.list[0].weather[0].icon}@2x.png`" 
  alt="Иконка погоды" />
    </td></tr>
    <tr><td>
     <p class="day">Второй день:</p>
     <p>Температура:{{ weather_data.list[8].main.temp }}</p>
     <p>Влажность:{{ weather_data.list[8].main.humidity }}</p>
     <p>Давление:{{ weather_data.list[8].main.pressure }}</p>
     <p>Описание:{{ weather_data.list[8].weather[0].description }}</p>
     <img 
  :src="`https://openweathermap.org/img/wn/${weather_data.list[8].weather[0].icon}@2x.png`" 
  alt="Иконка погоды" />
    </td></tr>
    <tr><td>
     <p class="day">Третий день:</p>
     <p>Температура:{{ weather_data.list[16].main.temp }}</p>
     <p>Влажность:{{ weather_data.list[16].main.humidity }}</p>
     <p>Давление:{{ weather_data.list[16].main.pressure }}</p>
     <p>Описание:{{ weather_data.list[16].weather[0].description }}</p>
     <img 
  :src="`https://openweathermap.org/img/wn/${weather_data.list[16].weather[0].icon}@2x.png`" 
  alt="Иконка погоды" />
    </td></tr>
    <tr><td>
     <p class="day">Четвёртый день:</p>
     <p>Температура:{{ weather_data.list[24].main.temp }}</p>
     <p>Влажность:{{ weather_data.list[24].main.humidity }}</p>
     <p>Давление:{{ weather_data.list[24].main.pressure }}</p>
     <p>Описание:{{ weather_data.list[24].weather[0].description }}</p>
     <img 
  :src="`https://openweathermap.org/img/wn/${weather_data.list[24].weather[0].icon}@2x.png`" 
  alt="Иконка погоды" />
    </td></tr>
    <tr><td>
     <p class="day">Пятый день:</p>
     <p>Температура:{{ weather_data.list[32].main.temp }}</p>
     <p>Влажность:{{ weather_data.list[32].main.humidity }}</p>
     <p>Давление:{{ weather_data.list[32].main.pressure }}</p>
     <img 
  :src="`https://openweathermap.org/img/wn/${weather_data.list[32].weather[0].icon}@2x.png`" 
  alt="Иконка погоды" />
    </td></tr>
  </table>
  </div>
  </template>
  <script>
  export default {
   name: 'App',
   data(){
    return{
     weather_data:null
    }
   },
   mounted(){
    
  fetch("https://api.openweathermap.org/data/2.5/forecast?lat=56.50&lon=60.35&appid=5aabb0813a2a69e1ca65a89ecae8e3fd&lang=ru&units=metric")
    .then(resp=>resp.json())
    .then(json=>{
     this.weather_data=json;
    })
   },
   methods:{
    city(sity){
     
  fetch(`https://api.openweathermap.org/data/2.5/forecast?lat=${sity.target.value.split(",")[0]}&lon=${sity.target.value.split(",")[1]}&appid=5aabb0813a2a69e1ca65a89ecae8e3fd&lang=ru&units=metric`)
    .then(resp=>resp.json())
    .then(json=>{
     this.weather_data=json;
    });
   },
   components: {
   
   }
   }}
  </script>
  <style>
  #app {
   text-align: center;
   font-family: Helvetica;
  }
  select {
    font-family: Helvetica;
    font-size: 14px;
  }
  table{
   border-top: 2px dotted rgb(84, 77, 175);
   border-bottom: 2px dotted rgb(84, 77, 175);
  margin: 0% auto;
  margin-top: 2%;
  }
  .day {
    font-size: 20px;
    font-weight: bold;
    color: blueviolet;
  }
  td{
   border-top: 2px dotted rgb(84, 77, 175);
   border-bottom: 2px dotted rgb(84, 77, 175);
  }
  h1 {
    color: rgb(165, 62, 168);
  }
  h2 {
    color:rgb(233, 24, 233);
  }
  </style>
