<template>
  <div class="card">
    <div class="flip-card-inner">
      <div class="flip-card-front">
        <img :src="getImage" :alt="title" />
      </div>
      <div class="flip-card-back">
        <h3>
          Titolo:
          <span class="ligther">{{title }}</span>
        </h3>
        <h4>
          Titolo Originale:
          <span class="lighter">{{
           titleOriginal
          }}</span>
        </h4>
        <p v-if="getFlag()">
          <img class="flag" :src="getFlag" :alt="item.original_language" />
        </p>
        <p class="lighter" v-else>Lingua: {{ item.original_language }}</p>
        <p>
          Voto:{{ getVote }}
          <i
            class="fa-star yellow"
            v-for="star in 5"
            :key="star"
            :class="star <= getVote ? 'fas' : 'far'"
          ></i>
        </p>
        <p class="lighter" v-if="item.overview">
          <span class="fs-4">Overview: </span>{{ item.overview }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: ["item"],
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
      if (this.lang.includes(this.item.original_language)) {
        this.pathFlag = require("../assets/img/" +
          this.item.original_language +
          ".png");
      }
      return this.pathFlag;
    },
  },
  computed: {
    title(){
      return this.item.title || this.item.name;
    },
    titleOriginal(){
      return  this.item.original_title || this.item.original_name;
    },
    /**
     * @return  path {String} for img cover or a default img
     */
    getImage() {
      if (!this.item.poster_path) return require("../assets/img/poster.png");
      return "https://image.tmdb.org/t/p/w342" + this.item.poster_path;
    },
    /**
     * @return  conversion vote average 5 star  ceil rounded
     */
    getVote() {
      return Math.ceil(this.item.vote_average / 2);
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
  .yellow {
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

.flip-card-front,
.flip-card-back {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden; /* Safari */
  backface-visibility: hidden;
}
.flip-card-front img {
  width: 100%;
  height: 100%;
}

.flip-card-back {
  overflow-y: scroll;
  scrollbar-width: none; //Mozilla
  -ms-overflow-style: none; /*Edge IE*/
  background-color: $dark-color;
  color: $light-color;
  transform: rotateY(180deg);
}
</style>