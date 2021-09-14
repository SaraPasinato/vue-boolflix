<template>
  <div id="app">
    <header id="main-header">
      <!-- header contains  search components and logo -->
      <div class="row container">
        <img src="./assets/img/logo.png" alt="logo">
        <div class="filter-control">
          <Select :items="genres" @getGenre="getAllGenre"/>
          <Search  @searchMovie="search" :btnText="btnText" />
        </div>  </div>
    </header>
      <!-- main contains Gallery components with cards inside it -->
    <main>
      <Gallery :items="catalogsInput" />
    </main>
  </div>
</template>

<script>
import Search from "./components/Search.vue";
import Select from "./components/Select.vue";
import Gallery from "./components/Gallery.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    Select,
    Search,
    Gallery,
  },
  data() {
    return {
      baseUri: "https://api.themoviedb.org/3/",
      apiKey: "dd4f41ba1a167ca7033fd2dead8221ef",
      movies: [],
      series: [],
      genresMovie: [],
      genresSeries:[],
      btnText: "Cerca per Titolo",
    };
  },
  computed:{
    catalogsInput(){
      return  [...this.movies, ...this.series];
    },
     genres(){
          this.genresSeries.forEach(genre => {
          if (!this.genresMovie.id=== genre.id)  return this.genresMovie.push(genre);
        });

        return this.genresMovie;
     },
  },
  methods: {
    getAllGenre() {
        this.getApiList("genre/movie/list", "genresMovie");
        this.getApiList("genre/tv/list", "genresSeries");
    },
    /**
     * @param text  {String}  for query API
     * @param type  {String}  get one or more  API call
     */
    search(text) {
      // controllo stringa vuota
      if (!text) this.movies = this.series = 0;

        this.getApi(text, "search/movie", "movies");
        this.getApi(text, "search/tv", "series");
     
    },
    /**
     * @param text {String} query text
     * @param endpoint {String} endpoint to concat
     * @param type {String}  to ref to arr
     */
    getApi(text, endpoint, type) {
      axios
        .get(this.baseUri + endpoint, {
          params: {
            api_key: this.apiKey,
            query: text,
            language: "it-IT",
          },
        })
        .then((res) => {
          this[type] = res.data.results;

        })
        .catch((err) => {
          console.log(err);
        });
    },

    getApiList(endpoint, type) {
      axios
        .get(this.baseUri + endpoint, {
          params: {
            api_key: this.apiKey,
            language: "it-IT",
          },
        })
        .then((res) => {
          this[type] = res.data.genres;

        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style lang="scss">
  @import "assets/scss/style.scss";
#main-header{
  background-color:$dark-color;
  height: 100px;
  width:100%;

  position: fixed;
  top: 0;
  left: 0;
  z-index: 1;
  .filter-control,
  .row{
  display: flex;
  height: 100%;
  justify-content: space-between;
  align-items: center;
  }

  img{
    height:100%;
    width: 15%;
  };
}
</style>
