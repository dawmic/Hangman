<script setup>
import { ref, computed } from "vue";
import GameOverPopup from "./GameOverPopup.vue";
import VictoryPopup from "./VictoryPopup.vue";
import Words from "./Words.vue";
import Figure from "./Figure.vue";
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
  number_of_lives = ref(6),
  word_to_guess = ref("- - -"),
  correct_letters = ref([]);

const testWord = ref("");

const getWrongLetter = (letter) => {
  if (word_to_guess.value.indexOf(letter.toLowerCase()) == -1)
    selected_letters.value.push(letter);
};

const getCorrectLetter = (letter) => {
  if (word_to_guess.value.indexOf(letter.toLowerCase()) > -1)
    correct_letters.value.push(letter);
};
const checkLetter = (key) => {
  console.log(key);
  getWrongLetter(key);
  getCorrectLetter(key);
  if (word_to_guess.value.indexOf(key.toLowerCase()) == -1) {
    document.querySelector(`[data-key=${key}]`).classList.add("wrong-letter");
    number_of_lives.value--;
  }
  if (word_to_guess.value.indexOf(key.toLowerCase()) > -1) {
    document.querySelector(`[data-key=${key}]`).classList.add("good-letter");
  }
};

const wrong_selected_letters = computed(() => [
  ...new Set(selected_letters.value),
].join(','));
const hided_word = computed(() => word_to_guess.value.toUpperCase().split(""));
const victory_status = computed(
  () =>
    [...new Set(correct_letters.value)].length ==
    [...new Set(word_to_guess.value.toUpperCase().split(""))].length
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

const getWordToGuess = (val) => (word_to_guess.value = val);
</script>
<template>
  <header>
    <h1 class="game-header">Hangman Game</h1>
    <p class="game-header__paragraph">
      Try to find the hidden word by typing a letter each time of your choice.
    </p>
  </header>
  <main class="game-container">
    <Figure :number_of_lives="number_of_lives" />
    <Words @wordToGuess="getWordToGuess($event)" />
    <Transition>
      <GameOverPopup v-if="number_of_lives < 1" :correct_word="word_to_guess" />
    </Transition>
    <Transition><VictoryPopup v-if="victory_status" /></Transition>
    <p class="selected-letters">
      Incorrect: {{ wrong_selected_letters }}
    </p>
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
.game-header {
  font-size: 2.8rem;
  font-weight: 600;
  letter-spacing: 2px;
  color: #25d622;
  text-align: center;
  font-family: "Courier New", Courier, monospace;
}
 
.game-header__paragraph {
  font-size: 1.6rem;
  text-align: center;
  margin: 1rem 0;
}
.game-container {
  // position: relative;
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
      height: 3.3rem;
      width: 3.3rem;
      border: 2px solid #bac2ba;
      border-radius: 0.8rem;
      margin: 0.5rem;
      text-align: center;
      line-height: 3rem;
      font-size: 1.76rem;
      transition: 0.3s;
      cursor: pointer;
      -webkit-animation: tracking-in-expand 0.7s
        cubic-bezier(0.215, 0.61, 0.355, 1) 0.7s both;
      animation: tracking-in-expand 0.7s cubic-bezier(0.215, 0.61, 0.355, 1)
        0.7s both;
      &:hover {
        scale: 1.1;
        background-color: lightgray;
        color: #282828;
      }
    }
  }

  .hide-word-container {
    display: flex;
    flex-direction: row;
    gap: 0.7rem;
    flex-wrap: wrap;
    justify-content: center;
    margin-top: 2rem;

    .hided-letter {
      border-bottom: 2px solid #bac2ba;
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
  background-color: #b31b1b;
}
.good-letter {
  background-color: #018749;
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
