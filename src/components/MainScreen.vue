<template>
  <div class="container">
    <div class="row justify-content-center align-items-center">
      <div class="col">
        <h1 class="text-center">{{msg}}</h1>
      </div>
    </div>
    <div class="row justify-content-center align-items-center">
      <div class="col-6">
        <div class="input-group">
          <input type="text" class="form-control" placeholder="Enter city..." aria-label="Enter city..." v-model="search" @keyup.enter="getCity" />
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
      seen: false
    }
  },
  methods: {
    getCity() {
      this.search = this.search.trim();
      this.search !== '' ? this.getWeatherData(this.search) : console.log('zzzz');
    },
    getWeatherData(cityName) {
      console.log('api.openweathermap.org/data/2.5/weather?q=' + cityName + '&units=metric&APPID=' + apiKey);
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
</style>
