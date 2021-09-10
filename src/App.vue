<template>
  <div id="app">
    <Header @searchMovie="searchMovie" />
    <main>
      <Gallery />
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
      baseUri: "https://api.themoviedb.org/3/search/movie",
      apiKey: "dd4f41ba1a167ca7033fd2dead8221ef",
      movies: [],
    
    };
  },
  methods: {
    searchMovie(text) {
      this.getApi(text);
    },
    getApi(text) {
      axios
        .get(this.baseUri,{
          params: {
            api_key: this.apiKey,
            query:text,
            language: "it-IT"
          }
        })
        .then((res) => {
          this.movies = res.data.results;
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
