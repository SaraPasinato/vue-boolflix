<template>
  <div>
      <input type="text" placeholder="Ricerca" v-model.trim="currentText" @keydown.enter="$emit('searchMovie',currentText,'all')" @keyup.enter="reset()">
      <button @click="$emit('searchMovie',currentText,'all')">{{btnText ||'Cerca'}}</button>
  </div>
</template>

<script>
export default {
 name:'Search',
 props:['btnText'],
 data(){
     return{
         currentText:'',
     }
 },
 methods:{
     reset(){
         this.currentText='';
     }
 }
}
</script>

<style>
button{
    display: none;
}
</style>