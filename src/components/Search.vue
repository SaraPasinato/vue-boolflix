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
     /**
      * @return resetting currentText var
      */
     reset(){
         this.currentText='';
     }
 }
}
</script>

<style lang="scss">
@import '../assets/scss/vars.scss';
button{
    display: none;
}

input{
    display: block;
    width: 100%;
    padding: .375rem .75rem;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: $dark-color;
    background-color: $light-color;
    background-clip: padding-box;
    border: 1px solid $light-color;
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    border-radius: .25rem;
    transition: border-color .15s ease-in-out,box-shadow .15s ease-in-out;

}

</style>