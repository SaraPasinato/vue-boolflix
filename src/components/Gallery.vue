<template>
  <section id="gallery">
   <div class="card" v-for="movie in movies" :key="movie.id">
       <h3>{{movie.title}}</h3>
       <h4>{{movie.original_title}}</h4>
       <p>{{movie.original_language}}</p>
       <p>{{movie.vote_average}}</p>
   </div>
  </section>
</template>

<script>

export default {
    name:'Gallery',
    props:['movies'],
}
</script>

<style>
#gallery{
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    
}
.card{
  border:2px solid black;  
  flex-basis: 25%;  
}
</style>