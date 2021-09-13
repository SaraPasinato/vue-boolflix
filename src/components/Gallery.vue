<template>
  <section id="gallery" class="container">
   <div class="row" >
       <div class="col" v-for="movie in movies" :key="movie.id" >
           <Card :movie="movie" />
       </div>
   </div>
  </section>
</template>

<script>
import Card from './Card.vue';
export default {
    name:'Gallery',
    props:['movies'],
    components:{
        Card,
    }
}

</script>

<style>
.row{
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
}

.col{
    flex-basis: calc(100%/5);
    padding: 15px;
}
</style>