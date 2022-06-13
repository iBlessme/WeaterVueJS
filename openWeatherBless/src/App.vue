//HTML
<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''">
    <main>
      <div class="search-box">
        <input type="text" class="search-bar" v-model="query" @keypress="fetchWeater" placeholder="Введите название города">
      </div>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">
            {{ weather.name }}, {{ weather.sys.country }}
          </div>
            <div class="date">{{ dateBuilder() }}</div>
        </div>
          <div class="weather-box">
            <div class="temp">{{ Math.round(weather.main.temp )}}°C </div>
            <div class="weather">{{weather.weather[0].main}}</div>
          </div>
      </div>
    </main>
  </div>
</template>



<script>
export default{
  name: "App",
  data() {
    return{
      api_key: "c64eb2aaa11ec500a5fac588c1f8c5d7",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather : {},
    };
  },


  methods: {
    fetchWeater(e){
      if(e.key == "Enter"){
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then((res) => {
          return res.json();
        })
        .then(this.setResult)
        console.log(this)
      }
    },

    setResult(res){
      this.weather = res;
    },

    dateBuilder(){
      let d = new Date();
    let mounths = [
      'Января',
      'Февраля',
      'Марта',
      'Апреля',
      'Мая',
      'Июня',
      'Июля',
      'Августа',
      'Сентября',
      'Октября',
      'Ноября',
      'Декабря',
    ];

    let days = [
      'Воскресение',
      'Понедельник',
      'Вторник',
      'Среда',
      'Четверг',
      'Пятница',
      'Суббота',
    ];

    let day = days[d.getDay()];
    let date = d.getDate();
    let mounth = mounths[d.getMonth()];
    let year = d.getFullYear();

    return `${day}, ${date} ${mounth} ${year}` 
    }
  }
}
</script>



<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto+Mono:ital@1&display=swap');
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body{
  font-family: 'Roboto Mono', monospace;
  font-weight: bolder;
}
#app{
  background-image: url('./assets/cool.jpg');
  filter: blur();
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}

#app.warm{
  background-image: url('./assets/hot.png');
}

main{
  min-height: 100vh;
  padding: 25px;

  background-image: linear-gradient(to bootom,rgba(0, 0, 0, 0.25),rgba(0, 0, 0, 0.75),);
}

.search-box{
width: 100%;
margin-bottom: 30px;
}
.search-box .search-bar{
  text-align: center;
  font-weight: bold;
  display: block;
  width: 100%;
  padding: 15px;

  color: rgb(38, 38, 36);
  font-size: 30px;
  appearance: none;
  border: none;
  outline: none;
  background: none;

  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.3);
  border-radius: 0px 20px 20px 20px;
  transition: 0.4s;
}

.search-box .search-bar:focus{
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.5);
  background-color: rgba(255, 255, 255, 0.65);
  border-radius: 20px 20px 0px 20px;
}

.location-box .location{
  color: #fff;
  font-size: 32px;
  font-weight: bolder;
  text-shadow: 1px 1px 2px black;
  text-align: center;
}

.location-box .date{
  color: #fff;
  font-size: 30px;
  font-weight: bolder;
  text-shadow: 1px 1px 2px black;
  text-align: center;
}

.weather-box{
  text-align: center;
}

.weather-box .temp{
  display: inline-block;
  padding: 10px 25px;
  color: aliceblue;
  font-size: 95px;
  font-weight: bolder;
  text-shadow: 1px 1px 2px black;
  background-color: rgba(0, 0, 0, 0.5);
  border-radius: 20px;
  margin: 30px 0px;
}

.weather-box .weather{
  color: #fff;
  font-size: 40px;
  font-weight: bolder;
  text-shadow: 1px 1px 2px black;
}
.weather-wrap{
  background-color: rgba(0, 0, 0, 0.3);
  border-radius: 20px;
  padding: 90px;
  
}




</style>
