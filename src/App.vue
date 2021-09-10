<template>
  <div id="app">
    <Header @searchMovie="search" />
    <main>
      <Gallery :movies="catalogs"/>
    </main>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Gallery from "./components/Gallery.vue";
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      baseUri: "https://api.themoviedb.org/3/search/",
      apiKey: "dd4f41ba1a167ca7033fd2dead8221ef",
      movies:[],
      series:[],
     catalogs:[],
    };
  },
  methods: {
    search(text,type) {
      if(type ==='all'){
       this.getApi(text,'movie');
       this.getApi(text,'tv');
       this.catalogs=[...this.movies,...this.series];
      }else{
        this.catalog=this.getApi(text,type);
      }
       
    },
    getApi(text,type) {
      axios
        .get(this.baseUri+type,{
          params: {
            api_key: this.apiKey,
            query:text,
            language: "it-IT"
          }
        })
        .then((res) => {
          if(type==='movie'){
            this.movies= res.data.results;
          }else{
            this.series= res.data.results;
          }

        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
  components: {
    Header,
    Gallery,
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
