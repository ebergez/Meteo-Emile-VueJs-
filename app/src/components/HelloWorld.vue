<template>
<div>
  <div class="toCenter">
    <h2>Enter a city and press enter to get it's weather info (city name has to be in english)</h2>
    <input v-model="message" @keypress.enter="sendMessage()" type="text">
    <div
      v-for="data in datas" :key="data.name"
    >
      <ul class="datas">
        <li>City : {{datas.name}}</li>
        <li>Temperature : {{datas.temperature}}</li>
        <li>{{datas.humidity}}</li>
        <li>{{datas.time}}</li>
      </ul>
     
    </div>
  </div>
  
</div>
     


</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      message : "",
      info : null,
      datas: []
    };
  },
  methods: {
    sendMessage(){
    this.response = []
    axios.get(`http://api.weatherstack.com/current?access_key=bee1004e26126f984fa45749fdd48453&query=${this.message}`)
    .then((response)=>{
      console.log(response)
      this.datas = response.data
      this.message = ''
    })
    }
  },
  mounted () {
  }
};
</script>