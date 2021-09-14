<template>
  <div class="me-3">
      <select v-model="currentGenre" @focus="$emit('getGenre')" @click="$emit('searchByGenre',currentGenre)">
          <option value="">All</option>
          <option v-for="item in items" :key="item.id" :value="item.id">{{item.name}}</option>
         
      </select>
  </div>
</template>

<script>
export default {
 name: 'Select',
 props:['items'],
 data(){
     return {
         currentGenre:'',
     }
 },
}
</script>
<style lang='scss'>

@import '../assets/scss/vars';
 select{
    display: block;
    width: 200px;
    padding: .375rem 2.25rem .375rem .75rem;
    -moz-padding-start: calc(0.75rem - 3px);
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: $primary-color;
    background-color: $light-color;
    background-repeat: no-repeat;
    background-position: right .75rem center;
    background-size: 16px 12px;
    border: 1px solid $dark-color;
    border-radius: .25rem;
    transition: border-color .15s ease-in-out,box-shadow .15s ease-in-out;
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
 }

 .me-3{
     margin-right:1.2rem;
 }
</style>