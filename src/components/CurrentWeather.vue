<template>
  <section class="container">
    <!-- Date -->
    <p class="date">{{ getCurrentDate(weather.current.dt) }}</p>
    <p>Current Weather Conditions in Malta</p>

    <div class="flex-container">
      <!-- Main Section -->
      <section class="main-info">
        <!-- Weather Icon -->
        <div class="svg">
          <WeatherIcon
            :currentWeather="weather.current.weather[0].description"
          />
        </div>

        <!-- Temperature & Conditions -->
        <div class="temp">
          <h3 class="degrees">{{ Math.round(weather.current.temp) }}°C</h3>
          <p>
            High: {{ Math.round(weather.daily[0].temp.max) }}°C | Low:{{ " " }}
            {{ Math.round(weather.daily[0].temp.min) }}°C
          </p>
          <p>
            {{
              getWeatherConditions(
                weather.current.weather[0].main,
                weather.current.weather[0].description
              )
            }}
          </p>
        </div>
      </section>

      <!-- Extra Info Section -->
      <section class="extra-info">
        <div class="flex-group">
          <p>UV</p>
          <p>{{ Math.round(weather.current.uvi) }}</p>
        </div>
        <div class="flex-group">
          <p>Wind Speed</p>
          <p>
            {{ getWind(weather.current.wind_deg, weather.current.wind_speed) }}
            kts
          </p>
        </div>
        <div class="flex-group">
          <p>Humidity</p>
          <p>{{ Math.round(weather.current.humidity) }}%</p>
        </div>
        <div class="flex-group">
          <p>Pressure</p>
          <p>{{ Math.round(weather.current.pressure) }}hpa</p>
        </div>
      </section>
    </div>
  </section>
</template>

<script>
import { getCurrentDate, getWeatherConditions, getWind } from "../utils";
import WeatherIcon from "../components/WeatherIcon";

export default {
  name: "CurrentWeather",
  props: {
    weather: Object,
  },
  methods: {
    getCurrentDate,
    getWeatherConditions,
    getWind,
  },

  components: { WeatherIcon },
};
</script>

<style scoped>
.container {
  background-color: rgba(0, 0, 0, 0.75);
  border-radius: 10px;
  width: 100%;
  max-width: 1024px;
  margin: 0 auto;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.flex-container {
  width: 100%;
  display: flex;
  flex-direction: column;
}

.main-info {
  flex-basis: 100%;
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 2rem 0;
}

.main-info:after {
  content: "";
  position: absolute;
  bottom: 0;
  left: 15%;
  width: 70%;
  border-bottom: 2px solid rgba(255, 255, 255, 0.15);
}

.date {
  font-size: 1.5rem;
  margin-bottom: 0.5rem;
}

.svg {
  width: 15rem;
  padding: 1rem;
}

.temp {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.temp p:nth-child(3) {
  margin-bottom: 0;
}

.degrees {
  font-size: 5rem;
  margin-bottom: 0.5rem;
}

p {
  font-size: 1.2rem;
  margin-bottom: 0.5rem;
}

.extra-info {
  flex-basis: 100%;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 1rem;
  padding: 2rem 0;
  justify-content: space-between;
}

.flex-group {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.flex-group p:first-of-type {
  font-weight: 600;
  margin-bottom: 0.25rem;
}

.flex-group p:nth-child(2) {
  font-size: 1rem;
}

@media (min-width: 1024px) {
  .main-info {
    flex-direction: row;
    justify-content: center;
    flex-basis: 60%;
  }
  .main-info:after {
    bottom: 15%;
    right: 0;
    left: unset;
    height: 70%;
    border-bottom: none;
    border-right: 2px solid rgba(255, 255, 255, 0.15);
  }

  .extra-info {
    flex-basis: 40%;
    place-items: center;
    grid-gap: 0;
  }

  .flex-container {
    flex-direction: row;
  }
}
</style>
