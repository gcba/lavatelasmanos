<template>
      <div class="flex-container1">
        <div class="inner-container1">
          <h1>Canciones</h1>
          <b-input-group class="mt-3">
            <b-form-input v-model="cancion" placeholder="Canción"></b-form-input>
          </b-input-group>
          <b-input-group class="mt-3">
            <b-form-input v-model="artista" placeholder="Artista"></b-form-input>
          </b-input-group>
          <b-button class="pb-2 mt-3" v-on:click="callGeniusApi()">Buscar</b-button>
          <Lyrics :lyrics="letra"/>
        </div>
      </div>
</template>

<script>
import Lyrics from "@/components/Lyrics.vue";
// import { getLyrics } from "genius-lyrics-api";
import axios from 'axios';

export default {
  name: "Buscador",
  data() {
    return {
      cancion: "",
      artista: "",
      letra: [],
      info: {}
    };
  },
  components:{
    Lyrics
  },
  methods: {
    // callGeniusApi() {
    //   const options = {
    //     apiKey: "9VyPZTthc2yB42unifChcbqkLev4JFKGzkzQXYi9UBjo_j87R-LIbaHys2KwAKu7", // genius developer access token
    //     title: this.cancion,
    //     artist: this.artista,
    //     optimizeQuery: true
    //   };
    //   getLyrics(options).then(lyrics => {
    //     lyrics = lyrics.split('\n')
    //     this.letra = lyrics.filter(n=>n && !n.startsWith('['));
    //   })
    // },
    callGeniusApi() {
      axios
      .get('https://api.genius.com/search?q=paranoid&access_token=9VyPZTthc2yB42unifChcbqkLev4JFKGzkzQXYi9UBjo_j87R-LIbaHys2KwAKu7')
      // .get('https://api.genius.com/oauth/authorize?'+
      //                                                 'client_id=tI-b_xaAtcPl0HD9HlH-_OsytshvmruhM2KzkbtDJGMMwiCExZ6l2dXt5Jti1r64&'+
      //                                                 'redirect_uri=http://localhost:8080&'+
      //                                                 'scope=annotation&'+
      //                                                 'state=200&'+
      //                                                 'response_type=code')
      .then(response => (this.info = response))
    }
  }
};
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
.flex-container1{
  display: flex;
  justify-content: space-between;
}

</style>
