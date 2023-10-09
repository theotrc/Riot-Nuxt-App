<template>
  <div>
  
    <!-- <img src="https://static.bigbrain.gg/assets/lol/riot_static/13.19.1/img/champion/d.png" alt="champions"> -->
    <div>
      <v-text-field v-model="textInput" label="Entrez votre texte"></v-text-field>
      <v-btn @click="valider">Valider</v-btn>
    </div>
      <p>{{ texte }}</p>
      

     
        <div v-for="game in allyTeam">
        
        <v-col>
        <v-container>
          <v-card :class="game[0].win ? 'green-card' : 'red-card'">
            
            <v-card-text>
            <v-row> 
              <v-col class="d-flex align-center">
                <v-col>
                    <p>{{ game[0].gameMode }}</p>
                    <p v-if="game[0].win">win</p>
                    <p v-else>loss</p>
                    <p>{{ game[0].duration }} min</p>
                  </v-col>
                     
                    </v-col>
                    <v-col class="text-center d-flex align-center">
                      <v-row>
                          <img class="champImg" v-if="champions" :src="`https://static.bigbrain.gg/assets/lol/riot_static/13.19.1/img/champion/${game[0].championName}.png`" :alt="game[0].championName">
                      
                        <v-col>
                          <img class="spellImg" :src="`http://ddragon.leagueoflegends.com/cdn/13.19.1/img/spell/${findSpellName(game[0].summoner1Id)}.png`" :alt="game[0].championName">
                        
                        
                          <img class="spellImg"  :src="`http://ddragon.leagueoflegends.com/cdn/13.19.1/img/spell/${findSpellName(game[0].summoner2Id)}.png`" :alt="game[0].championName">
                        </v-col>
                      </v-row>
                      
                    </v-col>
                    <v-col class="text-center d-flex align-center">
                      <v-row>
                        <img class="itemImg" v-if="game[0].item0 != 0" :src="`https://ddragon.leagueoflegends.com/cdn/13.19.1/img/item/${game[0].item0}.png`" :alt="game[0].item0">
                        <img class="itemImg" v-if="game[0].item1 != 0" :src="`https://ddragon.leagueoflegends.com/cdn/13.19.1/img/item/${game[0].item1}.png`" :alt="game[0].item1">
                        <img class="itemImg" v-if="game[0].item2 != 0" :src="`https://ddragon.leagueoflegends.com/cdn/13.19.1/img/item/${game[0].item2}.png`" :alt="game[0].item2">
                        <img class="itemImg" v-if="game[0].item3 != 0" :src="`https://ddragon.leagueoflegends.com/cdn/13.19.1/img/item/${game[0].item3}.png`" :alt="game[0].item3">
                        <img class="itemImg" v-if="game[0].item4 != 0" :src="`https://ddragon.leagueoflegends.com/cdn/13.19.1/img/item/${game[0].item4}.png`" :alt="game[0].item4">
                        <img class="itemImg" v-if="game[0].item5 != 0" :src="`https://ddragon.leagueoflegends.com/cdn/13.19.1/img/item/${game[0].item5}.png`" :alt="game[0].item5">
                        <img class="itemImg" v-if="game[0].item6 != 0" :src="`https://ddragon.leagueoflegends.com/cdn/13.19.1/img/item/${game[0].item6}.png`" :alt="game[0].item6">

                      </v-row>
                    </v-col>
              <v-col class="d-flex align-center">
                <v-col class="text-right">
                  <p class="summonerName" v-for="player in game">
                    <img class="champImgAlly" v-if="champions" :src="`https://static.bigbrain.gg/assets/lol/riot_static/13.19.1/img/champion/${player.championName}.png`">
                    <nuxt-link :to="`/stats/${player.summonerName}`">{{ player.summonerName }} </nuxt-link>
                  </p>
                  <v-btn @click="toggleCard(game)"> ^ </v-btn>
                </v-col>
              </v-col>
            </v-row>
            <v-col v-if="game[0].isExpanded">
              
              <v-col >
                  <div class="gameDescribe" v-for="player in game">
                    
                      <v-row>
                        <img class="champImg2" v-if="champions" :src="`https://static.bigbrain.gg/assets/lol/riot_static/13.19.1/img/champion/${player.championName}.png`">
                        <v-col cols="2">
                          <img class="spellImg" :src="`http://ddragon.leagueoflegends.com/cdn/13.19.1/img/spell/${findSpellName(player.summoner1Id)}.png`" :alt="summoner">
                          <img class="spellImg"  :src="`http://ddragon.leagueoflegends.com/cdn/13.19.1/img/spell/${findSpellName(player.summoner2Id)}.png`" :alt="summoner">
                        </v-col>
                      <v-col>
                        {{ player.summonerName }}
                        {{ player.kills }} /
                        {{ player.assists }} /
                        {{ player.deaths }}
                      </v-col>
                      <v-col cols="6">
                      <v-row>
                          <img class="itemImg" v-if="player.item0 != 0" :src="`https://ddragon.leagueoflegends.com/cdn/13.19.1/img/item/${player.item0}.png`" :alt="player.item0">
                          <img class="itemImg" v-if="player.item1 != 0" :src="`https://ddragon.leagueoflegends.com/cdn/13.19.1/img/item/${player.item1}.png`" :alt="player.item1">
                          <img class="itemImg" v-if="player.item2 != 0" :src="`https://ddragon.leagueoflegends.com/cdn/13.19.1/img/item/${player.item2}.png`" :alt="player.item2">
                          <img class="itemImg" v-if="player.item3 != 0" :src="`https://ddragon.leagueoflegends.com/cdn/13.19.1/img/item/${player.item3}.png`" :alt="player.item3">
                          <img class="itemImg" v-if="player.item4 != 0" :src="`https://ddragon.leagueoflegends.com/cdn/13.19.1/img/item/${player.item4}.png`" :alt="player.item4">
                          <img class="itemImg" v-if="player.item5 != 0" :src="`https://ddragon.leagueoflegends.com/cdn/13.19.1/img/item/${player.item5}.png`" :alt="player.item5">
                          <img class="itemImg" v-if="player.item6 != 0" :src="`https://ddragon.leagueoflegends.com/cdn/13.19.1/img/item/${player.item6}.png`" :alt="player.item6">

                        </v-row>
                      </v-col>
                      </v-row>
                      <v-col>
                        
                      </v-col>
                      
                  
                  </div>
                  <v-btn @click="toggleCard(game)"> ^ </v-btn>
                </v-col>
              </v-col>
          </v-card-text>
          </v-card>
          </v-container>

          </v-col>

        </div>
        


  
       


    <nuxt-link to="/"></nuxt-link>

    <nuxt/>
  </div>
  
</template>

<script>
import axios from "axios"
export default {
  computed:{
    texte(){
      return this.$route.params.text;
    }
  },
  mounted(){
          this.championsRequest();
          this.spellsRequest();
          this.sumRequest(this.$route.params.text)
        },
    data(){


        return {
            userInfo: null,
            username:null,
            puuid:null,
            gamesInfo:[],
            gameId:null,
            allyTeam:[],
            ennemyTeam:[],
            champions:null,
            spellJson:null,


        }
    },

  methods: {
  toggleCard(game) {
      game[0].isExpanded = !game[0].isExpanded;
    },
  valider() {
      if (this.textInput.trim() !== '') {
        this.$router.push(`/stats/${encodeURIComponent(this.textInput)}`);
      }},

  updateUsername(value){ 
    this.username = value;
  },
  championsRequest() {
    axios.get(`https://ddragon.leagueoflegends.com/cdn/11.22.1/data/en_US/champion.json`)
      .then((response) => (this.champions= response.data.data))
  },
  spellsRequest(){
    axios.get(`https://ddragon.leagueoflegends.com/cdn/13.19.1/data/en_US/summoner.json`)
      .then((response) => (this.spellJson = response.data.data))
  },
  findSpellName(spellKey){
    const spellKeyStr = String(spellKey)
    const spell = Object.values(this.spellJson).find(spell => spell.key === spellKeyStr)
    if (spell){
      return spell.id
    }else{
      return "no spell found"
    }
  },
  sumRequest(username) {
    axios.get(`/api/v2/lol/summoner/v4/summoners/by-name/${username}?api_key=${process.env.RIOT_KEY}`)
      .then((response) => {
        this.userInfo = response.data;
        this.puuid = response.data.puuid;
        return this.gameRequest(this.puuid); // Return the promise from gameRequest
      })
      .then((gameResponse) => {
        const gameDetailPromises = gameResponse.map(gameID => this.gameDetails(gameID)); // Appelle gameDetails pour chaque ID et stocke les promesses
        return Promise.all(gameDetailPromises);
        
      })
      
      .catch((error) => console.log(error))
  },
    gameRequest(puuid) {
    return axios.get(`/api/v1/lol/match/v5/matches/by-puuid/${puuid}/ids?start=0&count=20&api_key=${process.env.RIOT_KEY}`)
      .then((response) => this.gameId = response.data)
      .catch((error) => console.log(error))
  },
    gameDetails(gameID){
      return axios.get(`/api/v1/lol/match/v5/matches/${gameID}?api_key=${process.env.RIOT_KEY}`)
      .then((response) => (this.getFilteredPlayers(response, this.puuid)))
      .catch((error) => console.log(error))
  },
    getFilteredPlayers(response, puuid){
      const players = response.data.info.participants ;
      const gameMode = response.data.info.gameMode ;
      const targetPlayer = players.find(player => player.puuid == puuid);
      const gameDuration = response.data.info.gameDuration /60;
      targetPlayer["gameMode"] = gameMode ;
      targetPlayer["duration"] = gameDuration.toFixed(0);
      targetPlayer["isExpanded"] = false;
      console.log(targetPlayer)
      const team = targetPlayer.teamId
      // const allyTeam = players.find(player => player.teamId == team);
      const game = []
      game.push(targetPlayer)
      for (const x of response.data.info.participants) {
        if (x.teamId == team && x.puuid != puuid) {
          game.push(x)
        } if (x.teamId != team) {
          this.ennemyTeam.push(x)
        }
        
        
      }
      this.allyTeam.push(game)
    }

}
}

</script>
<style>
input{
  color: white;
}
.gameDescribe{
  margin: 10px;
}
.champImg2{
  max-width:30%;
}
.champImg{
  max-width: 50%;
}
.itemImg{
  max-width: 20%;
}
.green-card{
  background-color: rgba(6, 222, 255, 0.3) !important;
  
}
.red-card:hover{
  cursor: pointer;
}
.green-card:hover{
  cursor: pointer;
}
.red-card{
  background-color: rgba(255, 0, 0, 0.3) !important;
}
.spellImg{
  max-width: 50%;
}
.summonerName{
  margin: 0 !important;
}
.champImgAlly{
  max-width: 10%;
}
</style>

 