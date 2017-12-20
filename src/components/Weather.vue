<template>
  <div class="container scrollmenu">
    <div class="row">
  		<div class="col">
  			<div class="weather-card one">
  				<div class="top">
  					<div class="wrapper">
  						<div class="mynav">
  							<a href="javascript:;"><span class="lnr lnr-chevron-left"></span></a>
  							<a href="javascript:;"><span class="lnr lnr-cog"></span></a>
  						</div>
  						<h1 class="heading">{{weather.weather[0].main}}</h1>
  						<h3 class="location">{{weather.name}}</h3>
  						<p class="temp">
  							<span class="temp-value">{{weather.main.temp}}</span>
  							<span class="deg">0</span>
  							<a href="javascript:;"><span class="temp-type">C</span></a>
  						</p>
              <img :src='"http://openweathermap.org/img/w/"+weather.weather[0].icon+".png"' width="80px"/>
              <p class="temp-value">
                <h3 class="location">Wind speed: {{weather.wind.speed}} m/s</h3>
                <h3 class="location">Pressure: {{weather.main.pressure}}</h3>
              </p>
            </div>
  				</div>
  				<div class="bottom">
  					<div class="wrapper">
              <div class="d-flex flex-row align-items-stretch">
                <div class="p-2 weather-button">
                  <button class="round-toggle button" @click='getWeather'>5 days</button>
                </div>
                <div class="p-2 weather-button">
                  <button class="round-toggle button">16 days</button>
                </div>
              </div>
  					</div>
  				</div>
  			</div>
  		</div>
  	</div>
    <div v-if='seen' class="container-fluid testimonial-group">
      <div class="row flex-row flex-sm-nowrap pt-3">
        <div v-for='item in filteredResult'>
          <item :data='item'></item>
        </div>
      </div>
    </div>
    <div v-if='seenSecond' class="container-fluid testimonial-group">
      <div class="row flex-row flex-sm-nowrap pt-3">
        <div v-for='item in result'>
          <item :data='item'></item>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Item from './Item.vue'

const apiKey = '53348de24a0f9e7ef16c4fa3d6d405c7';

export default {
  name: 'Weather',
  props: ['weather'],
  components: {
    Item
  },
  data () {
    return {
      msg: 'Welcome to weather app!',
      seen: false,
      seenSecond: false,
      result: [],
      filteredResult: [],
    }
  },
  methods: {
    filterWeather(obj) {
      console.log('=========================')
      if(obj.dt_txt.split(' ')[1] === '15:00:00') return true;
    },
    getWeather() {
    this.$http.get('http://api.openweathermap.org/data/2.5/forecast?q='+this.weather.name+'&units=metric&APPID='+apiKey).then(response => {
        // get body data
        this.result = response.body.list;
        this.filteredResult = this.result.filter(this.filterWeather);
        this.seen = true;
      }, response => {
        // error callback
        console.log('oooops');
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  body {
    font-family: 'Montserrat', sans-serif;
    background: #112233;
  }

  .weather-card {
    margin: 60px auto;
    height: 740px;
    width: 450px;
    background: #fff;
    box-shadow: 0 1px 38px rgba(0, 0, 0, 0.15), 0 5px 12px rgba(0, 0, 0, 0.25);
    overflow: hidden;
  }
  .weather-card .top {
    position: relative;
    height: 570px;
    width: 100%;
    overflow: hidden;
    background: url("https://s-media-cache-ak0.pinimg.com/564x/cf/1e/c4/cf1ec4b0c96e59657a46867a91bb0d1e.jpg") no-repeat;
    background-size: cover;
    background-position: center center;
    text-align: center;
  }
  .weather-card .top .wrapper {
    padding: 30px;
    position: relative;
    z-index: 1;
  }
  .weather-card .top .wrapper .mynav {
    height: 20px;
  }
  .weather-card .top .wrapper .mynav .lnr {
    color: #fff;
    font-size: 20px;
  }
  .weather-card .top .wrapper .mynav .lnr-chevron-left {
    display: inline-block;
    float: left;
  }
  .weather-card .top .wrapper .mynav .lnr-cog {
    display: inline-block;
    float: right;
  }
  .weather-card .top .wrapper .heading {
    margin-top: 20px;
    font-size: 35px;
    font-weight: 400;
    color: #fff;
  }
  .weather-card .top .wrapper .location {
    margin-top: 20px;
    font-size: 21px;
    font-weight: 400;
    color: #fff;
  }
  .weather-card .top .wrapper .temp {
    margin-top: 20px;
  }
  .weather-card .top .wrapper .temp a {
    text-decoration: none;
    color: #fff;
  }
  .weather-card .top .wrapper .temp a .temp-type {
    font-size: 85px;
  }
  .weather-card .top .wrapper .temp .temp-value {
    display: inline-block;
    font-size: 85px;
    font-weight: 600;
    color: #fff;
  }
  .weather-card .top .wrapper .temp .deg {
    display: inline-block;
    font-size: 35px;
    font-weight: 600;
    color: #fff;
    vertical-align: top;
    margin-top: 10px;
  }
  .weather-card .top:after {
    content: "";
    height: 100%;
    width: 100%;
    display: block;
    position: absolute;
    top: 0;
    left: 0;
    background: rgba(0, 0, 0, 0.5);
  }
  .weather-card .bottom {
    margin-top: 5%;
    padding: 0 30px;
    background: #fff;
  }

  .weather-card .bottom .weather-button {
    width: 50%;
    height: 100%;
  }

  .round-toggle{
    outline:none;
    box-shadow:none;
    border: none;
    width: 100px;
    height: 100px;
    font-size: 1.3em;
    border-radius: 100px;
  }

  .round-toggle.button {
    box-shadow: 0 14px 28px rgba(0,0,0,0.25), 0 10px 10px rgba(0,0,0,0.22);
    background: #6f5499;
    color: white;
  }

  .round-toggle.button:hover {
    transition: 1s;
    background: #9d74db;
    color: black;
  }

  .testimonial-group > .row {
    overflow-x: auto;
    white-space: nowrap;
    margin-bottom: 100px;
  }

</style>
