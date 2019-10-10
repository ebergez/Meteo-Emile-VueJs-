<template>
<div>
  <h1 class="mainTitle">Bienvenue à Emile Météo</h1>
  <p class="question">De quel ville souhaiter vous connaitre la météo ?</p>
  <div class="toCenter">
    <input v-model="message" @keypress.enter="sendMessage()" type="text" placeholder="London (Nom de ville en anglais)">
  </div>
      <div class="datas" v-if="datas.length !== 0 && !datas.error">
        <div class="dataSquares">
          <div class="dataSquare">
            <h3 class="squareTitle">Ville / City </h3>
            <div class="toCenterData">
              <h4>{{datas.location.name}}</h4>
            </div>
          </div>
          <div class="dataSquare">
            <h3 class="squareTitle">Pays / Country </h3>
            <div class="toCenterData">            
              <h4>{{datas.location.country}}</h4>
            </div>
            
          </div>
          <div class="dataSquare">
            <h3 class="squareTitle">Température  </h3>
            <div class="toCenterData">
              <h4>{{datas.current.temperature}}°C</h4>
            </div>
          </div>
          <div class="dataSquare">
            <h3 class="squareTitle">Observation </h3>
            <div class="toCenterData">
              <h4>{{datas.current.observation_time}}</h4>
            </div>            
          </div>
          <div class="dataSquare">
            <h3 class="squareTitle">Temps / Weather </h3>
            <div class="toCenterData">
              <img :src="datas.current.weather_icons" alt="">
            </div>
          </div>
          <div class="dataSquare">
            <h3 class="squareTitle">Humidité </h3>
            <div class="toCenterData">            
              <h4>{{datas.current.humidity}}g/m3</h4>
            </div>
          </div>
        </div>
      </div>
      <div v-if="datas.error">
        <p class="errorMessage">Nom Invalide</p>
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
