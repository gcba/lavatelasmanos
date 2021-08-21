<template>
<div>
  <div class="print">
    <div class="container">
      <div class="flex-container1">
        <div class="inner-container1">
          <h1>Lavate las manos <br> al compás de tu letra favorita</h1>
          <h2>Elegí tu canción favorita y lávate las manos mientras la cantás en 13 simples pasos.</h2>
        </div>

        <div class="inner-container2">
          <img src="../assets/logo.png" alt="">
        </div>
      </div>

      <div class="flex-container2" v-if="lyrics.length > 0">  
        <div v-for="n in 13" v-bind:key="n" class="card">
          <div class="img-container">
            <img :src="'/img/' + n + '.png'" alt="">
          </div>
          <p>{{lyrics[n]}}</p>
        </div>
      </div>
    </div>
    </div>
      <b-button class="pb-2 mt-3" v-if="lyrics.length > 0" v-on:click="print()">Descargar poster</b-button>
      <img v-if="output" :src="output">
  </div>
</template>

<script>
export default {
  name: "Lyrics",
  data(){
    return{
      imgUrl: '',
      output: null
    }
  },
  props: {
    lyrics: Array
  },
  methods:{
    print(){
    }
  }
};
</script>

<style scoped>

.container{
  width: 80vw;
  margin: 50px auto;
  padding: 20px 50px;
  border-radius: 10px;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
}

.flex-container1{
  display: flex;
  justify-content: space-between;
}


.inner-container2 > img{
  width: 100px;
  margin-top: 30px;
}

.flex-container2{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

h1, h2 {
  font-weight: normal;
  margin: 30px 0px;
}

.card{
  width: 19vw;
  box-sizing: border-box;
  margin: 20px 0px;
  text-align: center;

}

img {
  width: 100%;
}

.img-container{
  border: 5px solid #067ac1;
  border-radius: 5px;
}

@media screen and (max-width: 1024px){
  .card{
    min-width: 40%;
    margin: 20px 0px;
    text-align: center;
  }
}

h3 {
  margin: 40px 0 0;
}
</style>
