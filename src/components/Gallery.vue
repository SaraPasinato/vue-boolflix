<template>
  <section id="gallery" class="container">
   <div class="row" >
       <div class="col" v-for="item in items" :key="item.id" >
           <Card :item="item" />
       </div>
   </div>
  </section>
</template>

<script>
import Card from './Card.vue';
export default {
    name:'Gallery',
    props:['items'],
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