<template>
  <div class="col-4 weather-day">
    <div>
      <img :src='"http://openweathermap.org/img/w/"+data.weather[0].icon+".png"' alt="Card image cap">
    </div>
    <div class="weather-body">
      <div class="row justify-content-center align-items-center">
        <h5 class="text-center">{{data.dt_txt}}</h5>
      </div>
      <div class="row row-first text-center">
        <div class="col">
          temp min: {{data.main.temp_min}}
        </div>
        <div class="col">
          2
        </div>
      </div>
      <div class="row row-second text-center">
        <div class="col">
          temp max: {{data.main.temp_max}}
        </div>
        <div class="col">
          4
        </div>
      </div>
    </div>
  </div>
</template>

<script>
let moment = require('moment');
export default {
  name: 'Item',
  props: ['data'],
  data () {
    return {
      msg: 'Welcome to weather app!',
    }
  },
  created: function () {
    this.data.dt_txt = moment(this.data.dt_txt,('YYYY-MM-DD')).format('MMM Do YY');
  },
  methods: {
  }
}
</script>
<style scoped>

  .weather-day {
    max-width: 100%;
    width: 250px;
    margin-left: 10px;
    box-shadow: 0 14px 28px rgba(0,0,0,0.25), 0 10px 10px rgba(0,0,0,0.22);
  }

  .weather-day:last-child {
    margin-right: 10px;
  }

  .weather-body {
    margin-bottom: 10px;
    padding-bottom: 10px;
  }

  .row-first {
    margin-bottom: 10px;
  }

  .row-second {
  }

</style>
