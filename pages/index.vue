<template>
  <div>
    {{ info }}
    
    <input 
      :value="username"
      @input="event => this.username = event.target.value"/>
      <button
        @click="sumrequest(username)">Search</button>
    <nuxt-link to="/"></nuxt-link>

    <nuxt/>
  </div>
  
</template>

<script>
import axios from "axios"
export default {
    data(){
        return {
            info: null,
            username:null,

        }
    },


    methods: {
      mafonct(){ 
        console.log() 
      },
      sumrequest(username) {
        axios.get(`https://euw1.api.riotgames.com/tft/summoner/v1/summoners/by-name/${username}?api_key=${process.env.RIOT_KEY}`)
          .then((response) => (this.info = response.data))
          .then((response) => (console.log(response)))
          .catch((error) => console.log(error))
      }
    }

                }

</script>
<style>
input{
  color: white;
}
</style>

 