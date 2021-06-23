<template>
  <div>
    <main class="container">
      <div class="weather-card one">
        <div class="top">
          <div class="wrapper">
            <div class="mynav">
              <a href="javascript:;"><span class="lnr lnr-chevron-left"></span></a>
              <a href="javascript:;"><span class="lnr lnr-cog"></span></a>
            </div>
            <h3 class="location">{{ weather.name }}, {{ weather.sys.country }}</h3>
            <h4 class="location">{{ dateBuilder() }}</h4> 
            <p class="temp">
              <span class="temp-value">{{ Math.round(weather.main.temp) }}</span>
              <span class="deg">0</span>
              <a href="javascript:;"><span class="temp-type">C</span></a>
            </p>
            <h1 class="heading" v-if= "weather.weather[0].main == 'Clear'">Céu limpo</h1>
          </div>
        </div>
        
        <div class="bottom">
          <div class="wrapper">
            <ul class="forecast">
              <li class="active">
                <span class="info">Temperatura máxima</span>
                <span class="lnr lnr-arrow-up condition" style="color:red">
                  <span class="temp" style="color:black">{{ weather.main.temp_max }}<span class="deg">0</span><span class="temp-type">C</span></span>
                </span>
              </li>
              <li class="active">
                <span class="info">Temperatura mínima</span>
                <span class="lnr lnr-arrow-down condition" style="color:green">
                  <span class="temp" style="color:black">{{ weather.main.temp_min }}<span class="deg">0</span><span class="temp-type">C</span></span>
                </span>
              </li>                    
              <li class="active">
                <span class="info">Pressão</span>
                <span class="lnr lnr-cloud-download condition">
                <span class="temp">{{ weather.main.pressure }}</span>
                </span>
              </li>
              <li class="active">
                <span class="info">Humidade</span>
                <span class="lnr lnr-drop condition">
                  <span class="temp">{{ weather.main.humidity }}<span class="deg">0</span><span class="temp-type">C</span></span>
                </span>
              </li>
              </ul>
          </div>
        </div>
      </div>         
    </main>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      api_key: '95f0b99e0fc777e1b3ca573342075d2a',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      defaultCity: 'Mossoró',
      weather: {}
    }
  },
  created: function() {
fetch(`${this.url_base}weather?q=${this.defaultCity}&units=metric&APPID=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setResults);
  },
  methods: {
    fetchWeather (e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.defaultCity}&units=metric&APPID=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setResults);
      }
    },
    setResults (results) {
      this.weather = results;
    },
    dateBuilder () {
      let d = new Date();
      let months = ["Janeiro", "Fevereiro", "Março", "Abril", "Maio", "Junho", 
      "Julho", "Agosto", "Setembro", "Outubro", "Novembro", "Dezembro"];
      let days = ["Segunda", "Terça", "Quarta", "Quinta", "Sexta","Sabádo","Domingo"];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    },
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'montserrat', sans-serif;
}

#app {
  background-image: url('./assets/bg-2.jpg');
  background-size: cover;
  background-position: bottom;
}

main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom), rgba(0,0,0,0.25), rgba(0,0,0,0.75) ;
}


.grid-container {
  justify-content: space-around;
  display: grid;
  grid-template-columns: auto auto auto;
  padding: 10px;
}



@import url("https://fonts.googleapis.com/css?family=Montserrat:400,500,600,700,800,900");
@import url("https://cdn.linearicons.com/free/1.0.0/icon-font.min.css");
body {
  font-family: 'Montserrat', sans-serif;
  background: #112233;
}

.weather-card {
  margin: 60px auto;
  height: 740px;
  width: 450px;
  background: #fff;
  box-shadow: 0 1px 38px rgba(0, 0, 0, 0.15), 0 5px 12px rgba(0, 0, 0, 0.25);
  overflow: hidden;
}
.weather-card .top {
  position: relative;
  height: 570px;
  width: 100%;
  overflow: hidden;
  background: url("https://cdn.olhares.com/client/files/foto/big/540/5404643.jpg") no-repeat;
  background-size: cover;
  background-position: center center;
  text-align: center;
}
.weather-card .top .wrapper {
  padding: 30px;
  position: relative;
  z-index: 1;
}
.weather-card .top .wrapper .mynav {
  height: 20px;
}
.weather-card .top .wrapper .mynav .lnr {
  color: #fff;
  font-size: 20px;
}
.weather-card .top .wrapper .mynav .lnr-chevron-left {
  display: inline-block;
  float: left;
}
.weather-card .top .wrapper .mynav .lnr-cog {
  display: inline-block;
  float: right;
}
.weather-card .top .wrapper .heading {
  margin-top: 20px;
  font-size: 35px;
  font-weight: 400;
  color: #fff;
}
.weather-card .top .wrapper .location {
  margin-top: 20px;
  font-size: 21px;
  font-weight: 400;
  color: #fff;
}
.weather-card .top .wrapper .temp {
  margin-top: 20px;
}
.weather-card .top .wrapper .temp a {
  text-decoration: none;
  color: #fff;
}
.weather-card .top .wrapper .temp a .temp-type {
  font-size: 85px;
}
.weather-card .top .wrapper .temp .temp-value {
  display: inline-block;
  font-size: 85px;
  font-weight: 600;
  color: #fff;
}
.weather-card .top .wrapper .temp .deg {
  display: inline-block;
  font-size: 35px;
  font-weight: 600;
  color: #fff;
  vertical-align: top;
  margin-top: 10px;
}
.weather-card .top:after {
  content: "";
  height: 100%;
  width: 100%;
  display: block;
  position: absolute;
  top: 0;
  left: 0;
  background: rgba(0, 0, 0, 0.4);
}
.weather-card .bottom {
  padding: 0 30px;
  background: #fff;
}
.weather-card .bottom .wrapper .forecast {
  overflow: hidden;
  margin: 0;
  font-size: 0;
  padding: 0;
  padding-top: 20px;
  max-height: 155px;
}
.weather-card .bottom .wrapper .forecast a {
  text-decoration: none;
  color: #000;
}
.weather-card .bottom .wrapper .forecast .go-up {
  text-align: center;
  display: block;
  font-size: 25px;
  margin-bottom: 10px;
}
.weather-card .bottom .wrapper .forecast li {
  display: block;
  font-size: 25px;
  font-weight: 400;
  color: rgba(0, 0, 0, 0.25);
  line-height: 1em;
  margin-bottom: 10px;
}
.weather-card .bottom .wrapper .forecast li .date {
  display: inline-block;
}
.weather-card .bottom .wrapper .forecast li .condition {
  display: inline-block;
  vertical-align: middle;
  float: right;
  font-size: 25px;
}
.weather-card .bottom .wrapper .forecast li .condition .temp {
  display: inline-block;
  vertical-align: top;
  font-family: 'Montserrat', sans-serif;
  font-size: 20px;
  font-weight: 400;
  padding-top: 2px;
}
.weather-card .bottom .wrapper .forecast li .condition .temp .deg {
  display: inline-block;
  font-size: 10px;
  font-weight: 600;
  margin-left: 3px;
  vertical-align: top;
}
.weather-card .bottom .wrapper .forecast li .condition .temp .temp-type {
  font-size: 20px;
}
.weather-card .bottom .wrapper .forecast li.active {
  color: rgba(0, 0, 0, 0.8);
}
.weather-card.rain .top {
  background: url("https://i.pinimg.com/originals/1e/ad/c4/1eadc4bb67c7efe73bb8fb40d1bb72c7.jpg") no-repeat;
  background-size: cover;
  background-position: center center;
}



</style>
