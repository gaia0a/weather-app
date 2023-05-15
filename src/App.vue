<template>
  <div id="app" :class="(typeof weather.main != 'undefined') && (weather.main.temp > 30 ? 'hot' : '' || weather.main.temp < 10 ? 'cold' : '')">
    <main>
      <div class="first-text">
        <p>Type in the name of the city you'd like to check the weather! ☺</p>
      </div>

      <div class="search-box">
        <input type="text" class="search-bar" placeholder="Search" v-model="query" @keypress="fetchWeather" />
      </div>

      <div class="weather-wrap" v-if="(typeof weather.main != 'undefined')">

        <div class="location-box">
          <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
          <div class="date">{{ dateBuilder() }}</div>
        </div>

        <div class=weather-box>
          <div class="temp">{{ Math.round(weather.main.temp) }}°C</div>
          <figure class="sunny" v-if="weather.weather[0].main == 'Clear'">
            <img src="./assets/sunny.gif" alt="Sunny"/>
          </figure>

          <figure class="rainy" v-if="weather.weather[0].main == 'Rain'">
            <img src="./assets/raining.gif" alt="Rain" />
          </figure>

          <figure class="drizzling" v-if="weather.weather[0].main == 'Drizzle'">
            <img src="./assets/raining.gif" alt="Drizzle" />
          </figure>

          <figure class="thunder" v-if="weather.weather[0].main == 'Thunderstorm'">
            <img src="./assets/thunder.gif" alt="Thunderstorm" />
          </figure>

          <figure class="cloudy" v-if="weather.weather[0].main == 'Clouds'">
            <img src="./assets/cloudy.gif" alt="Cloudy" />
          </figure>

          <figure class="misty" v-if="weather.weather[0].main == 'Mist'">
            <img src="./assets/misty.gif" alt="Misty" />
          </figure>

          <figure class="dusty" v-if="weather.weather[0].main == 'Dust'">
            <img src="./assets/misty.gif" alt="Dusty" />
          </figure>

          <figure class="sandy" v-if="weather.weather[0].main == 'Sand'">
            <img src="./assets/misty.gif" alt="Sandy" />
          </figure>

          <figure class="windy" v-if="weather.weather[0].main == 'Smoke'">
            <img src="./assets/windy.gif" alt="Smoke" />
          </figure>

          <figure class="smoky" v-if="weather.weather[0].main == 'Wind'">
            <img src="./assets/windy.gif" alt="Windy" />
          </figure>

          <figure class="ashy" v-if="weather.weather[0].main == 'Ash'">
            <img src="./assets/windy.gif" alt="Ashy" />
          </figure>

          <figure class="squall" v-if="weather.weather[0].main == 'Squall'">
            <img src="./assets/windy.gif" alt="Squall" />
          </figure>

          <figure class="foggy" v-if="weather.weather[0].main == 'Fog'">
            <img src="./assets/foggy.gif" alt="Foggy" />
          </figure>

          <figure class="hazy" v-if="weather.weather[0].main == 'Haze'">
            <img src="./assets/foggy.gif" alt="Haze" />
          </figure>

          <figure class="snow" v-if="weather.weather[0].main == 'Snow'">
            <img src="./assets/snowing.gif" alt="Snowy" />
          </figure>

          <figure class="tornado" v-if="weather.weather[0].main == 'Tornado'">
            <img src="./assets/tornado.gif" alt="Tornado" />
          </figure>

          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>

      </div>

    </main>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      api_key: 'd8cc2afd0d3297fab226b899e738e122',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },
  methods: {
    fetchWeather(e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setResults);
      }
    },
    setResults(results) {
      this.weather = results;
    },
    dateBuilder() {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day}${','} ${month} ${date}${','} ${year}`;
    }
  }
}
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  overflow-y: hidden;
}

#app {
  width: 100%;
  height: 100vh;
  background-color: #fff4df;
  transition: 0.5s;
}

#app.hot {
  background-color: rgb(255, 83, 20);
}

#app.cold {
  background-color: rgb(149, 185, 203);
}

main {
  width: 100%;
}

.first-text {
  text-align: center;
  padding-top: 7%;
}

.search-box {
  padding-top: 30px;
  margin-bottom: 20px;
}

.search-box .search-bar {
  display: block;
  margin: auto;
  width: 40%;
  min-width: 350px;
  height: 70px;
  background-color: #000;
  color: #fff;
  border: 3px solid #000;
  border-radius: 50px;
  padding: 1em;
  transition: 0.5s;
  outline: none;
}

.search-box .search-bar::placeholder {
  color: #ffffffa7;
}

.location-box {
  margin: 30px 0;
}

.location-box .location {
  text-align: center;
  font-size: 3rem;
  font-weight: 700;
  margin: 10px 0;
  text-transform: uppercase;
}

.location-box .date {
  text-align: center;
}

.weather-box {
  text-align: center;
}

.weather-box figure img {
  width: 12%;
  min-width: 150px;
  margin: 1vw;
}

.weather-box .temp {
  font-size: 1.8rem;
  font-weight: 800;
}

.weather-box .weather {
  font-style: italic;
}

@media screen and (max-width:768px) {
  .first-text {
    padding-top: 10%;
  }
}

@media screen and (max-width:450px) {
  .first-text {
    width: 70%;
    margin: auto;
    padding-top: 15%;
  }
}

@media screen and (max-width:400px) {
  .first-text {
    padding-top: 100px;
  }

  .search-box {
    padding-top: 20px;
    margin-bottom: 10px;
  }

  .search-box .search-bar {
    min-width: 250px;
    height: 60px;
  }

  .location-box .location {
    font-size: 2rem;
  }
}

@media screen and (max-height:540px) {
  body {
    overflow-y: scroll;
  }

  #app {
    height: 100%;
    background-color: #fff;
  }

  .first-text {
    padding-top: 30px;
  }

  .weather-box .weather {
    padding-bottom: 50px;
  }
}
</style>