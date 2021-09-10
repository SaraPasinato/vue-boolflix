<template>
  <div class="card" >
               <h3>{{movie.title}}</h3>
               <h4>{{movie.original_title}}</h4>
               <p>{{movie.original_language}}</p>
               <p>{{movie.vote_average}}</p>
           </div>
</template>

<script>
export default {
 name:'CardMovie',
 props:['movie'],
}
</script>

<style>

.card{
  border:2px solid black;  
}
</style>