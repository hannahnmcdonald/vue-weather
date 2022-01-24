<!-- Markup -->
<template>
  <div id='app'>
    <main>
      <h1 style = "color: white; text-align: center;"> Vue Weather </h1>
      <div class="search-box">
        <input 
          type="text" 
          class="search-bar" 
          placeholder=" City Search"
          v-model="query"
          @keypress="fetchWeather" />
      </div>
      <div class="row weather-wrap" v-if ="typeof weather.main != 'undefined'">
        <div class="card location-box" style="width: 18rem; margin: auto; text-align: center">
          <div class="card-body">
            <h5 class="card-title location">{{ weather.name }}, {{ weather.sys.country }}</h5>
            <p class="card-text date">{{ dateBuilder() }}</p>
            <!-- <img id="img"/> -->
            <p class="card-text temp">{{ Math.round(weather.main.temp) }} °F </p>
            <p class="card-text weather">{{ weather.weather[0].main }} </p>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
// JS Code //

  export default {
    name: 'App',
    data () {
      return {
        api_key: 'c6c69e1807c116c6d2751b910241be75',
        url_base: 'https://api.openweathermap.org/data/2.5/',
        query: '',
        weather: {}
      }
    },
    methods: {
      fetchWeather (e) {
        // On key press but ONLY if enter is pressed
        if (e.key == "Enter") {
          // fetch url with url base & api key plus query location
          fetch(`${this.url_base}weather?q=${this.query}&units=imperial&APPID=${this.api_key}`)
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
        let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
        let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
        let day = days[d.getDay()];
        let date = d.getDate();
        let month = months[d.getMonth()];
        let year = d.getFullYear();
        return `${day} ${date} ${month} ${year}`;
      }
    }
  }
</script>

<style>
/* CSS */
/* Bring in google fonts */
  @import url('https://fonts.googleapis.com/css2?family=Quicksand:wght@300;400&family=Zen+Maru+Gothic:wght@300&display=swap');
  /* Reg CSS */
  * {
    margin: 0;
    padding: 0;
    box-size: border-box;
  }
  body {
    font-family: 'Quicksand', sans-serif;;
  }
  #app {
    background-image: url('./assets/bg.jpg');
    background-size: cover;
    background-position: bottom;
    transition: 0.4s;
  }
  main {
    min-height: 100vh;
    padding: 25px;
    background-image: linear-gradient(to bottom, rgba(0,0,0,0.25), rgba(0,0,0,0.35));
  }
  .search-box {
    width: 100%;
    margin-bottom: 30px;
  }
  .search-box .search-bar {
    display: block;
    margin: auto;
    margin-top: 2rem;
    padding: 15px;
    color: #313131;
    text-align: center;
    font-size: 20px;
    appearance: none;
    border: none;
    outline: none;
    background: none;
    box-shadow: 0px 0px 8px rgba(0,0,0,0.25);
    background-color: rgba(255,255,255,0.5);
    border-radius: 0px 16px 0px 16px;
    transition: 0.4s;
  }
  .search-box .search-bar:focus {
    box-shadow: 0px 0px 16px rgba(0,0,0,0.25);
    background-color: rgba(255,255,255,0.75);
    border-radius: 16px 0px 16px 0px;
  }
  .weather-box {
    text-align: center;
  }
  .weather-box .temp {
    display: inline-block;
    padding: 10px 25px;
    color: #FFF;
    font-size: 102px;
    font-weight: 900;
    background-color:rgba(255, 255, 255, 0.25);
    border-radius: 16px;
    margin: 30px 0px;
    box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  }
  .weather-box .weather {
    color: #FFF;
    font-size: 48px;
    font-weight: 700;
    font-style: italic;
    text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  }
</style>
