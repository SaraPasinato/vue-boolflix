<template>
  <div id="app">
    <header id="main-header">
      <div class="row container">
        <img src="./assets/img/logo.png" alt="logo">
        <Search
          @searchMovie="search"
          :btnText="btnText"
        />
      </div>
    </header>
    <main>
      <Gallery :movies="catalogs" />
    </main>
  </div>
</template>

<script>
import Search from "./components/Search.vue";
import Gallery from "./components/Gallery.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    Search,
    Gallery,
  },
  data() {
    return {
      baseUri: "https://api.themoviedb.org/3/",
      apiKey: "dd4f41ba1a167ca7033fd2dead8221ef",
      movies: [],
      series: [],
      catalogs: [],
      btnText: "Cerca per Titolo",
    };
  },
  methods: {
    search(text, type) {
      // controllo stringa vuota
      if (!text) this.movies = this.series = 0;

      if (type === "all") {
        this.getApi(text, "search/movie", "movies");
        this.getApi(text, "search/tv", "series");
      } else if (type === "movie") {
        this.catalogs = this.getApi(text, "search/movie", "movies");
      } else {
        this.catalogs = this.getApi(text, "search/tv", "series");
      }
    },
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

          this.catalogs = [...this.movies, ...this.series];
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
