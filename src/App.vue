<script>
import axios from 'axios'
export default{
  data(){
    return{
      city:"",
      info:null
    }
  },
  computed:{
    cityName(){
      return "<"+ this.city+">"
    },
    showTemp(){
      return "Температура: "+ this.info.main.temp
    },
    showFels(){
      return "Ощущается как: "+ this.info.main.feels_like
    },
    showMin(){
      return "Мин Темп: "+ this.info.main.temp_min
    },
    showMax(){
      return "Макс Темп: "+ this.info.main.temp_max
    },
    showWind(){
      return "Скорость Ветра: "+ this.info.wind.speed+" м/c"
    }
  },
  methods:{
    getWeather(){
      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=acbbc1835a2efb12a6f7c4c118203860&units=metric`)
      .then(res =>(this.info=res.data))
    }
  }
}
</script>

<template>
    <div class="wrapper">
      <a href="http://127.0.0.1:8000/employers/export">Получить Excel</a> 
      <a href="http://127.0.0.1:8000/employers/export2">Получить Word</a>
      <h1>Узнай Погоду в Любом Городе</h1>
        <label for="c">Узнать Погоду в {{ city }}</label> <br>
          <input type="text" placeholder="Angarsk" id="c" v-on:input="city = $event.target.value">
          <button @click="getWeather">Проверить Погоду</button>
        <div v-if="info !=null">
        <p>{{ showTemp }}</p>
        <p>{{ showFels }}</p>
        <p>{{ showMin }}</p>
        <p>{{ showMax }}</p>
        <p>{{ showWind }}</p>
      </div>
    </div>
    
</template>

<style scoped>
body{
  width: 100%;
  height: 100vh;
  background-image: url("img/site/gabriel2.jpg");
  display:flex;
  justify-content: center;
  align-items: center;
  font-family: 'Roboto', sans-serif;
}

.wrapper{
  width: 900px;
  height: 500px;
  border-radius: 50px;
  background: rgba(255, 255, 255, 0.85);
  text-align: center;
  font-size: 30px;
  box-shadow: 0px 0px 15px rgba(0,0,0,0.2);
  transition: all 0.3s ease;
}

.wrapper:hover{
  transform: scale(1.01);
}

.wrapper h1{
  color: #333;
  margin-top: 20px;
}
.wrapper a{
  color: #333;
  margin-top: 20px;
  margin-left: 15px;
}

.wrapper label {
  margin-top: 20px;
  color: #555;
}

.wrapper input{
  margin-top: 15px;
  background: transparent ;
  border: 0;
  border-bottom: 3px solid darkgray;
  color: black;
  font-size: 14px;
  padding: 5px;
  outline: 0;
}

.wrapper button{
  margin-left: 20px;
  margin-top: 20px;
  padding: 10px 20px;
  border: none;
  background: #333;
  color: #fff;
  font-size: 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.wrapper button:hover{
  background: #555;
}

.wrapper p{
  color: #333;
  margin-top: 20px;
}

</style>
