<template>
  <div
    id="app"
    :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''"
  >
    <main class="main_page">
      <div class="main_wrapper">
        <a
          href="https://github.com/Pariola-droid/Weather-doctor"
          target="_blank"
          rel="no-opener"
          class="fixed animate__bounceIn"
        >
          <ion-icon name="logo-github"></ion-icon>
        </a>
        <div class="doc animate__bounceIn">
          <h3>Weather Doctor</h3>
        </div>

        <div class="search_box">
          <input
            type="text"
            name=""
            class="search animate__bounceIn"
            placeholder="Ask the weather doc"
            v-model="query"
            @keypress="fetchWeather"
          />
        </div>

        <div class="weather_wrap" v-if="typeof weather.main != 'undefined'">
          <div class="location_box">
            <div class="location animate__bounceIn">
              <div class="L">{{ weather.name }},</div>
              <div class="L">
                {{ weather.sys.country }}
              </div>
            </div>
            <div class="date animate__bounceIn">
              {{ dateBuilder() }}
            </div>
          </div>

          <div class="weather_box">
            <div class="temp animate__bounceIn">
              {{ Math.round(weather.main.temp) }}°c
            </div>
            <div class="weather animate__bounceIn">
              {{ weather.weather[0].main }}
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "WeatherC",
  data() {
    return {
      api_key: "413b11b282ea643091f6b3e1a502551f",
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
    dateBuilder() {
      let d = new Date();
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.main_page {
  height: 100vh;
  width: 100%;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
  display: grid;
  place-items: center;
  background-color: rgba(45, 87, 194, 0.05);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
}
.main_page .main_wrapper {
  height: 100vh;
  width: 500px;
  /* background: rgb(0, 255, 170); */
  padding: 0 2rem;
  display: flex;
  align-items: center;
  justify-content: space-around;
  flex-direction: column;
  /* background-color: rgba(45, 87, 194, 0.05); */
  /* backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px); */
}

.main_page .main_wrapper .fixed {
  position: fixed;
  top: 5%;
  right: 5%;
  text-decoration: none;
  animation-delay: 0s;
  animation-duration: 1s;
}

.main_page .main_wrapper .fixed ion-icon {
  font-size: 1.2rem;
  padding: 0.6rem;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 100%;
  color: #313131;
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: 0.4s;
}

.main_page .main_wrapper .fixed ion-icon:hover {
  transform: scale(1.1);
}

.main_wrapper .doc {
  width: 100%;
  height: auto;
  font-family: "Josefin Sans", sans-serif;
  color: #f5f5f5;
  text-shadow: 3px 6px 10px rgba(0, 0, 0, 0.25);
  animation-delay: 0s;
  animation-duration: 1s;
}

/* Search ======= Box */
.main_wrapper .search_box {
  /* margin: 0 auto; */
  width: 100%;
  height: 4rem;
}

.main_wrapper .search_box .search {
  width: 100%;
  height: 3.2rem;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 10px 0 10px 0;
  appearance: none;
  border: none;
  outline: none;
  color: #313131;
  padding: 1rem;
  transition: 0.4s;
  caret-color: #2c2c2c;
  font-size: 1rem;
  font-family: "Poppins", sans-serif;
  text-transform: capitalize;
  animation-delay: 0s;
  animation-duration: 1s;
}

.main_wrapper .search_box .search::placeholder {
  color: #2c2c2c;
  transition: 0.4s;
}

.main_wrapper .search_box .search:hover::placeholder {
  word-spacing: 4px;
}

.main_wrapper .search_box .search:focus,
.main_wrapper .search_box .search:hover {
  border-radius: 0 8px 0 8px;
  background-color: rgba(255, 255, 255, 0.75);
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
}

/* Weather ======= Wrap */
.main_wrapper .weather_wrap {
  width: 100%;
  height: auto;
}

/* Location ======= Box */
.main_wrapper .weather_wrap .location_box {
  margin: 6rem auto;
  width: 100%;
  height: auto;
  margin-top: -1rem;
  display: grid;
  place-items: center;
}

.main_wrapper .weather_wrap .location_box .location {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: auto;
  animation-delay: 0s;
  animation-duration: 1s;
  /* background: grey; */
}

.main_wrapper .weather_wrap .location_box .location .L {
  margin: 0 0.5rem;
  height: auto;
  text-transform: capitalize;
  padding: 1rem 0;
  font-size: 3rem;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
  font-weight: 500;
  color: #f5f5f5;
}

.main_wrapper .weather_wrap .location_box .date {
  width: 100%;
  height: auto;
  text-transform: capitalize;
  margin: 0.5rem auto;
  font-size: 2rem;
  word-spacing: 2px;
  color: #f5f5f5;
  animation-delay: 0s;
  animation-duration: 1s;
}

/* Weather ======= Box */
.main_wrapper .weather_wrap .weather_box {
  /* margin: auto; */
  width: 100%;
  height: auto;
  /* background: brown; */
  display: flex;
  align-items: center;
  justify-content: space-around;
  margin: 0 auto;
}

.main_wrapper .weather_wrap .weather_box .temp {
  height: 150px;
  width: 150px;
  padding: 1rem;

  display: grid;
  place-items: center;
  text-transform: capitalize;
  border-radius: 30px;
  margin: 0 auto;
  font-size: 3.8rem;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(45, 87, 194, 0.05);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: #f5f5f5;
  animation-delay: 0s;
  animation-duration: 1s;
}

.main_wrapper .weather_wrap .weather_box .weather {
  height: 150px;
  width: 150px;
  padding: 1rem;
  background: grey;
  display: grid;
  place-items: center;
  text-transform: capitalize;
  border-radius: 30px;
  margin: 0 auto;
  font-size: 2.8rem;
  font-weight: 900;
  text-shadow: 3px 6px 10px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: #f5f5f5;
  animation-delay: 0s;
  animation-duration: 1s;
}

@media only screen and (max-width: 500px) {
  .main_page .main_wrapper .fixed {
    top: 3%;
  }

  .main_wrapper .search_box .search {
    font-size: 0.9rem;
    height: 3.5rem;
  }
  .main_page .main_wrapper {
    width: 100%;
  }

  .main_page .main_wrapper {
    padding: 0 1rem;
  }

  .main_wrapper .weather_wrap .weather_box {
    justify-content: space-between;
  }

  .main_wrapper .weather_wrap .weather_box .temp {
    font-size: 3.4rem;
  }

  .main_wrapper .weather_wrap .weather_box .weather {
    font-size: 2.2rem;
  }

  .main_wrapper .weather_wrap .location_box .location .L {
    font-size: 2rem;
  }

  .main_wrapper .weather_wrap .location_box .date {
    font-size: 1.2rem;
  }
}

@media only screen and (max-width: 320px) {
  .main_wrapper .weather_wrap .weather_box .temp {
    width: 140px;
  }

  .main_wrapper .weather_wrap .weather_box .weather {
    width: 140px;
  }
}
</style>
