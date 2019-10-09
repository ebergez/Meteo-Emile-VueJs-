<template>
<div>
  <h1 >{{info}}</h1>
  <input v-model="message" @keypress.enter="sendMessage()" type="text">
  <li
  v-for="data in datas" :key="data.name"
  >
  <!-- {{data}} -->
  {{data.name}}
  {{data.temperature}}
  <!-- {{data.}} -->
  <pre>{{datas}}</pre>
  </li>
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