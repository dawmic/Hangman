<script setup>
import { computed } from "vue";
const props = defineProps(['number_of_lives']);
console.log(props.number_of_lives);
const activeFigure = computed(() => `chance-remained-${props.number_of_lives}`);

</script>
<template>
  <p>{{activeClass}}</p>
    <div class="figure-container"><img :class="activeFigure" src="../assets/hangman-figure.png" alt="game figure"></div>

</template>
<style lang='scss' scoped>
.figure-container{
    height: 20rem;
    width: 7.5rem;
    overflow: hidden;
    margin: 2rem 0;
    scale: 1.2;

}
  img{
  position: relative;

  }
  .chance-remained-6{
    left: 0px;
  }
  .chance-remained-5{
    left: -75px;
  } 
  .chance-remained-4{
    left: -150px;
  } 
  .chance-remained-3{
    left: -225px;
  } 
  .chance-remained-2{
    left: -300px;
  } 
  .chance-remained-1{
    left: -375px;
  } 
  .chance-remained-0{
    left: -450px;
  } 
</style>