<template>
  <div class="card">
    <h3>{{ movie.title || movie.name }}</h3>
    <h4>{{ movie.original_title || movie.original_name }}</h4>
    <p v-if="getFlag()">
      <img :src="pathFlag" :alt="movie.original_language" />
    </p>
    <p v-else>{{ movie.original_language }}</p>
    <p>{{ movie.vote_average }}</p>
    <img :src="getImage(movie.poster_path)" :alt="movie.title || movie.name">
  </div>
</template>

<script>
export default {
  name: "CardMovie",
  props: ["movie"],
  data() {
    return {
      lang: ["it", "en"],
      pathFlag: "",
    };
  },
  methods: {
    getFlag() {
      if (this.lang.includes(this.movie.original_language)) {
        this.pathFlag = require("../assets/img/" +
          this.movie.original_language +
          ".png");
      }
      return this.pathFlag;
    },

    getImage(path){
        if(!path) return ;
        return 'https://image.tmdb.org/t/p/w342'+path;
    }
  },
};
</script>

<style>
.card {
  border: 2px solid black;
}

img {
  width: 30px;
}
</style>