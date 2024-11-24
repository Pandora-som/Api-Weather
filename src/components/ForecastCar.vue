<template>
    <div class="card">
        
        <p><B>Дата и время </B>: {{ new Date(weather_date.dt*1000).toLocaleString() }}</p>
        <p> <B>Температура</B>: {{ weather_date.main.temp }} °C</p>
        <p><B>Влажность</B>: {{ weather_date.main.humidity  }}</p>
          <p><B>Давление</B>: {{ weather_date.main.pressure  }}</p>
          <p><B>Погода</B>: {{ weather_date.weather[0].description  }}</p>
        <img :src="`https://openweathermap.org/img/wn/${weather_date.weather[0].icon}@2x.png`" alt="Иконка погоды" />
    
    </div>
    
    </template>
    
    <script>
    export default{
    name:"ForecastCar",
    props:{
        weather_date:{
            type:Object
        }
    },
    
    }
    </script>
    
    <style scoped>
    .card{
        border: 7px dotted rgb(75, 17, 67);
        margin: 0% auto;
        margin-top: 2%;
        width: 400px;
        border-radius: 5%;
    }
    
    </style>
    
    
    