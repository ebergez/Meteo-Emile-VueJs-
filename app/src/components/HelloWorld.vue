<template>
<div>
  <h1 class="mainTitle">Bienvenue a Emile Météo</h1>
  <div class="toCenter">
    <input v-model="message" @keypress.enter="sendMessage()" type="text" placeholder="Paris">
  </div>
      <ul class="datas" v-if="datas.length !== 0">
        <li>City : {{datas.location.name}}</li>
        <li>Temperature : {{datas.current.temperature}}</li>
        <li>Humidity : {{datas.current.humidity}}</li>
        <li>Observed at : {{datas.current.observation_time}}</li>
      </ul>

  
</div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      message : "",
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
