<template>
  <div class="container" v-bind:class="[{centered:!seen},{base:seen}]">
    <div class="row justify-content-center align-items-center">
      <div class="col">
        <h1 class="text-center">{{msg}}</h1>
      </div>
    </div>
    <div class="row justify-content-center align-items-center">
      <div class="col-6">
        <div class="input-group">
          <input list="cities-list" type="text" class="form-control"
          placeholder="Enter city..." aria-label="Enter city..."
          v-model="search" @keyup.enter="getCity"/>
          <datalist id="cities-list">
            <option v-for='city in cities' v-bind:value="city.name + ','+city.country"/>
          </datalist>
          <span class="input-group-btn">
            <button class="btn btn-secondary" type="button">Go!</button>
          </span>
        </div>
      </div>
    </div>
    <div class="row">
      <weather v-if="seen" :weather="result"></weather>
    </div>
  </div>
</template>

<script>

import Weather from './Weather.vue'

const apiKey = '53348de24a0f9e7ef16c4fa3d6d405c7';

export default {
  name: 'MainScreen',
  components: {
    Weather
  },
  data () {
    return {
      msg: 'Welcome to weather app!',
      search: '',
      result: [],
      cities: [],
      deepSearch: '',
      seen: false
    }
  },
  created: function () {
    //this.loadCitiesList();
  },
  methods: {
    loadCitiesList() {
      this.$http.get('static/city.list.json').then(response => {
        // get body data
        console.log('asdasdasdsdsdasdasdasd')
        this.cities = response.body;
      }, response => {
        // error callback
        console.log('pwel nahoooooi');
      });
    },
    getCity() {
      this.search = this.search.trim();
      this.search !== '' ? this.getWeatherData(this.search) : console.log('zzzz');
    },
    getWeatherData(cityName) {
      this.$http.get('http://api.openweathermap.org/data/2.5/weather?q='+cityName+'&units=metric&APPID='+apiKey).then(response => {
        // get body data
        this.result = response.body;
        this.seen = true;
        console.log(this.result);
      }, response => {
        // error callback
        this.seen = false;
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  body {
    font-family: 'Montserrat', sans-serif;
  }
</style>

<style scoped>
  h1, h2 {
    font-weight: normal;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  a {
    color: #42b983;
  }

  .centered {
    margin-top: 50%;
  }

  .base {
    margin-top: 0;
    transition: margin-top 5s ease-in-out;
  }
</style>
