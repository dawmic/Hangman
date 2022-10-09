<script setup>
import { ref, computed } from "vue";
import GameOverPopup from "./GameOverPopup.vue";
import VictoryPopup from "./VictoryPopup.vue";
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

const selected_letters = ref([]),
  number_of_lives = ref(5),
  word_to_guess = "hangman",
  correct_letters = ref([]);

const getWrongLetter = (letter) => {
  if (word_to_guess.indexOf(letter.toLowerCase()) == -1)
    selected_letters.value.push(letter);
};

const getCorrectLetter = (letter) => {
  if (word_to_guess.indexOf(letter.toLowerCase()) > -1)
    correct_letters.value.push(letter);
};
const checkLetter = (key) => {
  console.log(key);
  getWrongLetter(key);
  getCorrectLetter(key);
  if (word_to_guess.indexOf(key.toLowerCase()) == -1) {
    document.querySelector(`[data-key=${key}]`).classList.add("wrong-letter");
    number_of_lives.value--;
  }
  if (word_to_guess.indexOf(key.toLowerCase()) > -1) {
    document.querySelector(`[data-key=${key}]`).classList.add("good-letter");
  }
};

const wrong_selected_letters = computed(() => [
  ...new Set(selected_letters.value),
]);
const hided_word = computed(() => word_to_guess.toUpperCase().split(""));
const victory_status = computed(
  () =>
    [...new Set(correct_letters.value)].length ==
    [...new Set(word_to_guess.toUpperCase().split(""))].length
);

window.addEventListener("keyup", (ev) => {
  const key = ev.key.toUpperCase();
  console.log(key);
  if (letters.includes(key)) {
    checkLetter(key);
  } else {
    return;
  }
});
</script>
<template>
  <Transition>
    <GameOverPopup v-if="number_of_lives < 1" :correct_word="word_to_guess" />
  </Transition>
  <Transition><VictoryPopup v-if="victory_status" /></Transition>
<header>
  <h1 class="game-header">Hangman</h1>
</header>
  <main class="game-container">
    <p class="selected-letters">{{ word_to_guess }}</p>
    <p class="selected-letters">
      wrong typed letters {{ wrong_selected_letters }}
    </p>
    <p class="selected-letters">{{ number_of_lives }}</p>
    <p class="selected-letters">correct letters: {{ correct_letters }}</p>
    <p class="selected-letters" v-if="number_of_lives == 0">GAME OVER</p>

    <div class="letter-container">
      <div
        :data-key="letter"
        class="letter-item"
        v-for="letter in letters"
        :key="letter"
        @click="checkLetter(letter, $event)"
      >
        {{ letter }}
      </div>
    </div>
    <div class="hide-word-container">
      <div v-for="letter in hided_word" class="hided-letter">
        <span
          class="hided-letter__item"
          :class="{ show: correct_letters.includes(letter) }"
          >{{ letter }}</span
        >
      </div>
    </div>
  </main>
</template>
<style lang="scss" scoped>
  .game-header{
    -webkit-animation: tracking-in-expand 0.7s cubic-bezier(0.215, 0.610, 0.355, 1.000) both;
	        animation: tracking-in-expand 0.7s cubic-bezier(0.215, 0.610, 0.355, 1.000) both;
  }
.game-container {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;

  .selected-letters {
    font-size: 2rem;
  }
  .letter-container {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    

    .letter-item {
      height: 3.2rem;
      width: 3.2rem;
      border: 2px solid black;
      border-radius: 0.8rem;
      margin: 1rem;
      text-align: center;
      color: black;
      line-height: 3rem;
      font-size: 1.76rem;
      transition: 0.3s;
      cursor: pointer;
      -webkit-animation: tracking-in-expand 0.7s cubic-bezier(0.215, 0.610, 0.355, 1.000) .7s both;
	        animation: tracking-in-expand 0.7s cubic-bezier(0.215, 0.610, 0.355, 1.000) .7s both;
      &:hover {
        scale: 1.1;
        background-color: lightgray;
      }
      &:active {
        background-color: lightgray;
        scale: 1.1;
      }
    }
  }

  .hide-word-container {
    display: flex;
    flex-direction: row;
    gap: 0.7rem;
    flex-wrap: wrap;
    justify-content: center;

    .hided-letter {
      border-bottom: 2px solid black;
      height: 2rem;
      width: 2rem;
      text-align: center;
      line-height: 0.5;
      font-size: 2rem;
      .hided-letter__item {
        opacity: 0;
        transition: 0.5s;
      }
    }
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

.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
.show {
  opacity: 1 !important;
}
</style>
