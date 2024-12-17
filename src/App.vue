<template>
  <div id="app">
    <h1>Weather App</h1>
    <div class="input">
      <input
        type="text"
        v-model="input"
        placeholder="Digite aqui..."
        v-on:keyup.enter="searchWeather" />
      <button @click="searchWeather">Buscar</button>
    </div>
    <div v-for="(weather, index) in weathers" :key="index">
      <p>{{ weather.temp_c }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      weathers: null,
      input: "",
    };
  },
  methods: {
    searchWeather() {
      axios
        .get(
          `http://api.weatherapi.com/v1/current.json?key=fb70673b1ac84af0a38233429241112&q=${this.input}&aqi=no`
        )
        .then((r) => (this.weathers = r.data));
      this.input = "";
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 40px;
  row-gap: 20px;
}

h1 {
  border-bottom: solid 4px #dc143c;
}

input {
  font-size: 1rem;
  padding: 5px 10px;
  background-color: transparent;
  color: white;
  border: 1px solid #dc143c;
  border-radius: 4px;
}

input:focus {
  outline: none;
}

.input {
  display: flex;
  column-gap: 10px;
}

.input button {
  font-size: 1rem;
  padding: 4px 8px;
  font-weight: bold;
  background: #dc143c;
  color: white;
  border: none;
  border-radius: 4px;
}

body {
  font-family: sans-serif;
  background: #272727;
  color: #fff;
}
</style>
