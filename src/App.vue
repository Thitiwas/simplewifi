<template>
  <div id="app">
    <h1>Scanwifi</h1><hr>
    <div v-for="show in data">
      <h4>name :         {{show.ssid}}        </h4>
      <h4>mac Address :  {{show.mac}}         </h4>
      <progress :value="(100+show.rssi)" max="100" class="rssi"></progress>
      <h4>rssi :         {{show.rssi}}     dBm</h4>
      <h4>Channel :      {{show.channel}}     </h4>
      <hr>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'App',
  data () {
    return {
      data: []
    }
  },
  mounted () {
    var vm = this
    setInterval(function () {
      axios.get('http://localhost:4000/scan').then(res => {
        vm.data = res.data
      })
    }, 5000)
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
