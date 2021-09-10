<template>
  <div class="card" >
               <h3>{{movie.title}}</h3>
               <h4>{{movie.original_title}}</h4>
               <p v-if="getFlag()"><img :src="pathFlag" :alt="movie.original_language"></p>
               <p v-else>{{movie.original_language}}</p>
               <p>{{movie.vote_average}}</p>
           </div>
</template>

<script>
export default {
 name:'CardMovie',
 props:['movie'],
 data(){
     return{
         lang:['it','en'],
         pathFlag:'',
     }
 },
 methods:{
     getFlag(){
         if(this.lang.includes(this.movie.original_language)){

           this.pathFlag= require("../assets/img/"+ this.movie.original_language+".png"); 
         }
          return this.pathFlag;

     },
 },
}
</script>

<style>

.card{
  border:2px solid black;  
}

img{
    width: 30px;
}
</style>