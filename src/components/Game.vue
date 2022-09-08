<script setup>
import { ref, computed } from "vue";
const letters = [
  "A",
  "B",
  "C",
  "D",
  "E",
  "F",
  "G",
  "H",
  "I",
  "J",
  "K",
  "L",
  "M",
  "N",
  "O",
  "P",
  "Q",
  "R",
  "S",
  "T",
  "U",
  "V",
  "W",
  "X",
  "Y",
  "Z",
];
const word_to_guess = "paragraph";

const selected_letters = ref([]); 
const number_of_lives = ref(5);
const displayWrongLetter = (letter) => {
 // if(word_to_guess.indexOf(letter) > -1) return;
 // else selected_letters.value.push(letter);
  //word_to_guess.indexOf(letter) > -1 ? 
  console.log(word_to_guess.indexOf(letter.toLowerCase()) > -1);
  if(word_to_guess.indexOf(letter.toLowerCase()) == -1) selected_letters.value.push(letter);

}
const checkLetter = (key) =>{
console.log(key.target.textContent);
displayWrongLetter(key.target.textContent);
if(word_to_guess.indexOf(key.target.textContent.toLowerCase()) == -1){
    key.target.classList.add('wrong-letter');
    number_of_lives.value--;
}
if(word_to_guess.indexOf(key.target.textContent.toLowerCase()) > -1){
    key.target.classList.add('good-letter');
}

}

const wrong_selected_letters = computed(() => [... new Set(selected_letters.value)] );
</script>
<template>
  <main class="game-container">
    <p class="selected-letters">{{ wrong_selected_letters }} </p>
    <p class="selected-letters">{{ number_of_lives }}</p>
    <p class="selected-letters" v-if="number_of_lives == 0">GAME OVER</p>
    
    <div
      class="letter-container"
      v-for="letter in letters"
      :key="letter"
      @click="checkLetter($event)"
    >
      {{ letter }}
    </div>
  </main>
</template>
<style lang="scss" scoped>
.game-container {
  flex-grow: 0.3;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;

  .selected-letters {
    color: black;
    font-size: 2rem;
  }
  .letter-container {
    height: 3rem;
    width: 3rem;
    border: 2px solid black;
    border-radius: 0.8rem;
    margin: 1rem;
    text-align: center;
    color: black;
    line-height: 3rem;
    font-size: 1.76rem;
  }
}
.wrong-letter {
  background-color: red;
  color: white !important;
}
.good-letter {
  background-color: green;
  color: white !important;
}
</style>
