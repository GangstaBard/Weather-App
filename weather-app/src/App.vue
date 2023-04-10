<template>
  <main>
    <div class="search-container">
      <div class="search-box">
        <input
          v-model="query"
          @keypress="fetchWeather"
          type="text"
          class="search-bar"
          placeholder="Seacrh..."
        />
      </div>
    </div>

    <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
      <div class="location-box">
        <div class="location">
          {{ weather.name }}, {{ weather.sys.country }}
        </div>
      </div>

      <div class="weather-box">
        <div class="temp">{{ Math.round(weather.main.temp) }}°</div>
        <div class="weather">{{ weather.weather[0].main }}</div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api_key: "2b7e4ee2fbe82e23e02685340a96e3f8",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
    };
  },
  methods: {
    fetchWeather(e) {
      if (e.key == "Enter") {
        fetch(
          `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then((res) => {
            return res.json();
          })
          .then(this.setResults);
      }
    },
    setResults(results) {
      this.weather = results;
    },
  },
};
</script>

<style lang="scss">
:root {
  font-size: 10px;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "Montserrat", sans-serif;
}

#app {
  background-image: url("@/assets/wallpaper.png");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}

main {
  min-height: 100vh;
  padding: 2.5rem;
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.25),
    rgba(0, 0, 0, 0.75)
  );
}

.search-container {
  @media only screen and (min-width: 35rem) {
    display: flex;
    justify-content: center;
  }
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 1.5rem;

  color: #313131;
  font-size: 2rem;

  appearance: none;
  background: none;
  border: none;
  outline: none;

  box-shadow: 0rem 0remr 0.8rem rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0 1.6rem 0 1.6rem;
  transition: 0.3s;

  @media only screen and (min-width: 35rem) {
    width: 100%;
  }
}

.search-box .search-bar:focus {
  box-shadow: 0rem 0rem 1.6rem rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 1.6rem 0 1.6rem 0;
}

.location-box .location {
  padding-top: 1rem;
  color: #fff;
  font-size: 3.2rem;
  font-weight: 500;
  text-align: center;
  text-shadow: 0.1rem 0.3rem rgba(0, 0, 0, 0.25);
}

.location-box {
  padding-top: 0.5rem;
  color: #fff;
  text-align: center;
  font-size: 2rem;
  font-weight: 300;
  font-style: italic;
}

.weather-box {
  padding-top: 0.5rem;
  text-align: center;
}

.weather-box .temp {
  color: #fff;
  display: inline-block;
  text-align: center;
  padding: 1rem 2.5rem;
  font-size: 10rem;

  text-shadow: 0.3rem 0.6rem rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 1.6rem;
  margin: 3rem 0rem;
  box-shadow: 0.3rem 0.6rem rgba(0, 0, 0, 0.25);
}

.weather-box .weather {
  color: #fff;
  text-align: center;
  font-size: 4.8rem;
  font-weight: 500;
  font-style: italic;
  text-shadow: 0.3rem 0.6rem rgba(0, 0, 0, 0.25);
}
</style>
