<template>
  <div class="card">
    <div class="flip-card-inner">
      <div class="flip-card-front">
        <img
          :src="getImage(movie.poster_path)"
          :alt="movie.title || movie.name"
        />
      </div>
      <div class="flip-card-back">
        <h3>
          Titolo:
          <span class="ligther">{{ movie.title || movie.name }}</span>
        </h3>
        <h4>
          Titolo Originale:
          <span class="lighter">{{
            movie.original_title || movie.original_name
          }}</span>
        </h4>
        <p v-if="getFlag()">
          <img class="flag" :src="pathFlag" :alt="movie.original_language" />
        </p>
        <p class="lighter" v-else>Lingua: {{ movie.original_language }}</p>
        <p>Voto: <span class="lighter star" v-html="renderStar()"></span></p>
        <p class="lighter" v-if="movie.overview">
          <span class="fs-4">Overview: </span>{{ movie.overview }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: ["movie"],
  data() {
    return {
      lang: ["it", "en"],
      pathFlag: "",
    };
  },
  methods: {
    /**
     * @return  path {String} for img flag
     */
    getFlag() {
      if (this.lang.includes(this.movie.original_language)) {
        this.pathFlag = require("../assets/img/" +
          this.movie.original_language +
          ".png");
      }
      return this.pathFlag;
    },
    /**
     * @return  path {String} for img cover or a default img 
     */
    getImage(path) {
      if (!path) return require("../assets/img/poster.png");
      return "https://image.tmdb.org/t/p/w342" + path;
    },
     /**
     * @return  conversion vote average 5 star  ceil rounded 
     */
    getVote() {
      return Math.ceil(this.movie.vote_average / 2);
    },
     /**
     * @return print stars {String}
     */
    renderStar() {
      const starSolid = this.getVote();
      let strStar = ``;
      for (let i = 0; i < 5; i++) {
        strStar +=
          i < starSolid
            ? `<i class="fas fa-star"></i>`
            : `<i class="far fa-star"></i>`;
      }
      return strStar;
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/vars";

.card {
  background-color: transparent;
  border-radius: 5px;
  color: $light-color;

  height: 300px;
  width: 250px;

  .lighter {
    font-weight: lighter;
  }
  .star {
    color: $star;
  }

  .fs-4 {
    font-size: 1.1em;
    font-weight: bold;
  }

  p,
  h3,
  h4 {
    margin: 25px;
  }

  img.flag {
    width: 30px;
  }

}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
  border-radius: 5px;
}

.card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

.flip-card-front,.flip-card-back {
  position: absolute;
  top:0;
  left:0;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden; /* Safari */
   backface-visibility: hidden;
}
.flip-card-front img{
  width:100%;
  height: 100%;
}

.flip-card-back {
 
  overflow-y: scroll;
  scrollbar-width: none;     //Mozilla
  -ms-overflow-style: none; /*Edge IE*/
  background-color: $dark-color;
  color: $light-color;
  transform: rotateY(180deg);
  
} 
</style>