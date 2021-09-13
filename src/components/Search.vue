<template>
  <div>
      <input type="text" placeholder="" v-model.trim="currentText" @keyup.enter="$emit('searchMovie',currentText,'all')">
      <button @click="$emit('searchMovie',currentText,'all')">{{btnText ||'Cerca'}}</button>
  </div>
</template>

<script>
export default {
 name:'Search',
 props:['placeholder','btnText'],
 data(){
     return{
         currentText:'',
     }
 },
}
</script>

<style>

</style>