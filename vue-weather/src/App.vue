<!-- Markup -->
<template>
  <div id='app'>
    <main>
      <h1 style = "color: white; text-align: center;"> Vue Weather </h1>
      <div class="search-box">
      <!-- Key press = v-on:keypress and will fire the fetchWeather fx -->
        <input 
          type="text" 
          class="search-bar" 
          placeholder=" City Search"
          v-model="query"
          @keypress="fetchWeather" />
      </div>
      <!-- v-if will only display this element (and its children) if the typeof returned is not undefined -->
      <div class="row weather-wrap" v-if ="typeof weather.main != 'undefined'">
      <!-- Current day forecast card -->
        <div class="card location-box" style="width: 18rem; margin: auto; text-align: center">
          <div class="card-body">
            <h5 class="card-title location">{{ weather.name }}, {{ weather.sys.country }}</h5>
            <p class="card-text date">{{ dateBuilder() }}</p>
            <!-- Able to use img src with v-bind vue directive. -->
            <img id="img" v-bind:src="weather.weather[0].icon" />
            <!-- Math.round rounds the temp to a whole number -->
            <p class="card-text temp"> Temperature: {{ Math.round(weather.main.temp) }} °F </p>
            <p class="card-text weather">{{ weather.weather[0].description }} </p>
            <p class="card-text weather"> Wind Speed: {{ weather.wind.speed }} MPH </p>
            <!-- Will pass this lat and lon into the fetch5Day fx -->
            <p class="card-text weather"> {{ weather.coord.lat }}, {{ weather.coord.lon }} </p>
          </div>
          <!-- 5 day forecast card that will populate from the forecast loop -->
          <div class="card location-box" style="width: 18rem; margin: auto; text-align: center">
          <div class="card-body">
            <p class="card-text date">{{ dateBuilder() }}</p>
            <!-- Able to use img src with v-bind vue directive. -->
            <img id="img" v-bind:src="weather.daily[i].weather.icon" />
            <!-- Math.round rounds the temp to a whole number -->
            <p class="card-text temp"> Temperature: {{ Math.round(weather.daily[i].temp.day) }} °F </p>
            <p class="card-text weather">{{ weather.daily[i].weather.description }} </p>
            <p class="card-text weather"> Wind Speed: {{ weather.daily[i].wind_speed }} MPH </p>
            <!-- <p class="card-text weather"> {{ weather.coord.lat }}, {{ weather.coord.lon }} </p> -->
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
// JS Code //
  export default {
    // "App" ties into our div id #app above in the template. Vue is currently only working with that div and all its children
    name: 'App',
    data () {
      return {
        // TO DO: Nest this api key in a .env. Still troubleshooting.
        api_key: 'c6c69e1807c116c6d2751b910241be75',
        url_base: 'https://api.openweathermap.org/data/2.5/',
        // Query (the city search) must be a string
        query: '',
        // Create the weather object
        weather: {}
      }
    },
    // FUNCTIONS: //
    methods: {
      // Fetches the current forecast just for day[0]
      fetchWeather (e) {
        // On key press but ONLY if enter is pressed
        if (e.key == "Enter") {
          // fetch url with url base & api key plus query location
          fetch(`${this.url_base}weather?q=${this.query}&units=imperial&APPID=${this.api_key}`)
            .then(res => {
              return res.json();
              // THEN execute next fx- setResults();
            }).then(this.setResults);
        }
      },
      // Sets the results inside our weather object that we declared above.
      setResults (results) {
        this.weather = results;
        // TO DO: Execute next fx for fetch5Day() + Bring it lat and lon query values
      },
      dateBuilder () {
        let d = new Date();
        let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
        let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
        let day = days[d.getDay()];
        let date = d.getDate();
        let month = months[d.getMonth()];
        let year = d.getFullYear();
        return `${day} ${month} ${date}, ${year}`;
      },
      // fetch5Day (lat, lon) {
      //   // fetch url with url base & api key plus query location
      //     fetch(`https://api.openweathermap.org/data/2.5/onecall?lat=${lat}&lon=${lon}&exclude=minutely,hourly,alerts&units=imperial&appid=${this.api_key}`)
      //       .then(res => {
      //         return res.json();
      //       }).then(this.setResults);
      // }
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
    font-family: 'Quicksand', sans-serif;
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
  .card {
    text-align: center;
    box-shadow: 0px 0px 8px rgba(0,0,0,0.25) !important;
    background-color: rgba(255,255,255,0.90) !important;
    border-radius: 0px 16px 0px 16px !important;
    transition: 0.4s !important;
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
