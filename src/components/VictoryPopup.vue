<script setup>
    import NewGameButton from './NewGameButton.vue'
</script>
<template>
  <div class="popup-container">
    <!--<a href="https://www.flaticon.com/free-icons/trophy" title="trophy icons">Trophy icons created by Freepik - Flaticon</a>-->
    <img
      class="popup-victory-image"
      width="128"
      height="128"
      src="../assets/trophy.png"
      alt="trophy"
    />
    <h1 class="popup-victory-header">Hooray</h1>
    <p class="popup-victory-paragraph">You guessed the password!</p>
    <NewGameButton>
     WANT MORE
      </NewGameButton>
  </div>
</template>
<style lang="scss" scoped>
.popup-victory-image {
    -webkit-animation: bounce-in-top 1.1s both;
	        animation: bounce-in-top 1.1s both;
}
.popup-victory-header {
  font-size: 4.2rem;
  font-weight: 700;
  letter-spacing: 1.5px;
  color: #ffffff;
  -webkit-animation: scale-in-center 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94)
    0.3s both;
  animation: scale-in-center 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94) 0.3s both;
}
.popup-victory-paragraph {
  color: #ffc93c;
  font-size: 2rem;
  font-weight: 500;
  -webkit-animation: scale-in-center 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94)
    0.6s both;
  animation: scale-in-center 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94) 0.6s both;
}
</style>
