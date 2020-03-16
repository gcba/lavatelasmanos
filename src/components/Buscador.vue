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
import { getLyrics } from "genius-lyrics-api";

export default {
  name: "Buscador",
  data() {
    return {
      cancion: "",
      artista: "",
      letra: []
    };
  },
  components:{
    Lyrics
  },
  methods: {
    callGeniusApi() {
      const options = {
        apiKey: "9VyPZTthc2yB42unifChcbqkLev4JFKGzkzQXYi9UBjo_j87R-LIbaHys2KwAKu7", // genius developer access token
        title: this.cancion,
        artist: this.artista,
        optimizeQuery: true
      };
      getLyrics(options).then(lyrics => {
        lyrics = lyrics.split('\n')
        this.letra = lyrics.filter(n=>n && !n.startsWith('['));
      })
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
