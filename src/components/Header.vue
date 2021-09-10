<template>
  <header>
      <input type="text" placeholder="Ricerca Films" v-model.trim="currentText">
      <button @click="$emit('searchMovie',currentText,'all')"> Cerca</button>
  </header>
</template>

<script>
export default {
 name:'Header',
 data(){
     return{
         currentText:'',
     }
 },
}
</script>

<style>

</style>