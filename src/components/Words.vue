<script setup>
import axios from "axios";
import { ref, computed } from "vue";

const emit = defineEmits(["wordToGuess"]);
const failed = ref(false);

const getRandomWord = async () => {
  try {
    const words = await axios.get("/words.json");
    const random_word = await computed(
      () =>
        words.data.words[Math.floor(Math.random() * words.data.words.length)]
    );
    emit("wordToGuess", random_word.value);
  } catch (err) {
    console.log(err);
    failed.value = true;
  }
};
getRandomWord();
</script>

<template>
  <p v-if="failed">Failed to fetch data.</p>
</template>

<style lang="scss" scoped></style>
