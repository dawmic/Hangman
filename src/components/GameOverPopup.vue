<script setup>
import NewGameButton from './NewGameButton.vue';
const props = defineProps(['correct_word']);
</script>
<template>
  <div class="popup-container">
    <img
     
      height="200"
      src="../assets/cropped_hangman_end.png"
      alt="game over hangman"
      class="popup-image"
    />
    <!--<a href="https://www.flaticon.com/free-icons/hangman" title="hangman icons">Hangman icons created by Smashicons - Flaticon</a> -->
    <h1 class="popup-header">GAME OVER</h1>
    <p class="popup-paragraph">The correct password is: <span class="popup-paragraph__key">{{props.correct_word}}</span></p>
    <NewGameButton>
     TRY AGAIN
      </NewGameButton>
  </div>
</template>
<style lang="scss">
// container styles are located in main.css
  .popup-image {
    -webkit-animation: bounce-in-top 1.1s both;
	        animation: bounce-in-top 1.1s both;
  }
  .popup-header {
    font-size: 4rem;
    font-weight: 700;
    letter-spacing: 3px;
    color: #ffffff;
   // animation: shake 0.82s cubic-bezier(0.36, 0.07, 0.19, 0.97) both;
   
	-webkit-animation: rotate-in-center 0.6s cubic-bezier(0.250, 0.460, 0.450, 0.940) 1s both;
	        animation: rotate-in-center 0.6s cubic-bezier(0.250, 0.460, 0.450, 0.940) 1s both;

  }
  .popup-paragraph{
    margin: 0 1rem;
    text-align: center;
font-size: 2rem;
color: #ececec;
font-weight: 500;
.popup-paragraph__key{
  font-size: 2.5rem;
  color: #ffc93c;
  font-weight: 600;
  letter-spacing: 1px;
}

  }
  
  




</style>
