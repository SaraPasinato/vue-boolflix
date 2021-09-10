<template>
  <section id="gallery">
   <div class="row">
       <div class="col" v-for="movie in movies" :key="movie.id" >
           <CardMovie :movie="movie"/>
       </div>
   </div>
  </section>
</template>

<script>
import CardMovie from './CardMovie.vue';
export default {
    name:'Gallery',
    props:['movies'],
    components:{
        CardMovie,
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
}
</style>