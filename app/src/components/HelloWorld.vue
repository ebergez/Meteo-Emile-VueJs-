<template>
<div>
  <h1 class="mainTitle">Bienvenue a Emile Météo</h1>
  <div class="toCenter">
    <input v-model="message" @keypress.enter="sendMessage()" type="text" placeholder="Paris">
  </div>
      <div class="datas" v-if="datas.length !== 0 && !datas.error">
        <div class="dataSquares">
          <div class="dataSquare">
            <h3 class="squareTitle">Ville </h3>
            <h4>{{datas.location.name}}</h4>

          </div>
          <div class="dataSquare">
            <h3 class="squareTitle">Température </h3>
            <h4>{{datas.current.temperature}}°C</h4>

          </div>
          <div class="dataSquare">
            <h3 class="squareTitle">Ressenti </h3>
            <h4>{{datas.current.feelslike}}°C</h4>

          </div>
          <div class="dataSquare">
            <h3 class="squareTitle">Observée à </h3>
            <h4>{{datas.current.observation_time}}</h4>

          </div>
          <div class="dataSquare">
            <h3 class="squareTitle">Temps </h3>
            <img :src="datas.current.weather_icons" alt="">
          </div>
          <div class="dataSquare">
            <h3 class="squareTitle">Humidité </h3>
            <h4>{{datas.current.humidity}}g/m3</h4>

          </div>
        </div>
      </div>
      <div v-if="datas.error">
        <p>Need real city</p>
      </div>

  
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
