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
import axios from 'axios';
import cio from 'cheerio';

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
    callGeniusApi() {
      axios
      .get(`https://api.genius.com/search?q=${this.cancion}${this.artista}&access_token=9VyPZTthc2yB42unifChcbqkLev4JFKGzkzQXYi9UBjo_j87R-LIbaHys2KwAKu7`)
      .then( (response) => {
        const hits = response.data.response.hits;
        if( hits.length > 0 ){
          console.log('encontre alggo');
          const results = hits.map(val => {
            const { full_title, path } = val.result;
            return { title: full_title, path };
          });


          const baseUrl    = 'https://cors-anywhere.herokuapp.com/https://www.genius.com';
          const lyricsUrl  = baseUrl + results[0].path;
              
          axios.get(lyricsUrl).then( (res) => {
            const $ = cio.load(res.data);
            const selector = $('div[class="lyrics"]');
            
            const lyrics = selector.text().trim().split('\n');
            this.letra = lyrics.filter(n=>n && !n.startsWith('['));
          });
        }
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
