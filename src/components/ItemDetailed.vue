<template>
  <div class="row justify-content-center align-items-center text-center">
    <div v-for='item of data' class="col-8">
      <div class="col-12">
        <div class="row justify-content-center align-items-center text-center">
          <h3>{{item.date}}</h3>
        </div>
        <div class="row">
            <table class="table table-striped">
              <thead>
                <tr>
                  <th class="w-20">Hours</th>
                  <th class="w-30">Weather</th>
                  <th class="w-25">t, <sup>o</sup>C</th>
                  <th class="w-25">Pressure</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for='subitem of item.buf'>
                  <th scope="row">{{subitem.dt_txt}}</th>
                  <td>
                    <img :src='"http://openweathermap.org/img/w/"+subitem.weather[0].icon+".png"' />
                    <p>{{subitem.weather[0].main}}</p>
                  </td>
                  <td>{{subitem.main.temp}}</td>
                  <td>{{subitem.main.pressure}}</td>
                </tr>
              </tbody>
            </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'item-detailed',
  props: ['data'],
  data () {
    return {
      msg: 'Welcome to weather app!',
    }
  },
  methods: {
  }
}
</script>
<style scoped>
 h3 {}
</style>
