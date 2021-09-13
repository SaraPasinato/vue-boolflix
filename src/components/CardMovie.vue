<template>
  <div class="card">
    <h3>{{ movie.title || movie.name }}</h3>
    <h4>{{ movie.original_title || movie.original_name }}</h4>
    <p v-if="getFlag()">
      <img :src="pathFlag" :alt="movie.original_language" />
    </p>
    <p v-else>{{ movie.original_language }}</p>
    <p>{{getVote()}}</p>
    <p v-html='renderStar()'></p>
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
        if(!path) return require("../assets/img/poster.png");
        return 'https://image.tmdb.org/t/p/w342'+path;
    },

    getVote(){
        return Math.ceil(this.movie.vote_average /2);
    },

    renderStar(){
        const starSolid=this.getVote();
        let strStar=``;
        for(let i=0; i<5; i++){
            strStar+=(i<starSolid)?`<i class="fas fa-star"></i>`:`<i class="far fa-star"></i>`;
        }
        return strStar;
    },
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