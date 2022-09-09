<script setup>

</script>
<template>
<div class="popup-container">
  <img width="128" height="128" src="../assets/hangman_go.png" alt="game over hangman" class="popup-image">
  <!--<a href="https://www.flaticon.com/free-icons/hangman" title="hangman icons">Hangman icons created by Smashicons - Flaticon</a> -->
  <p class="popup-paragraph">GAME OVER</p>
  <button class="popup-button">NEW WORD</button>
</div>
</template>
<style lang='scss' scoped>
  .popup-container{
    margin: 0;
    padding: 0;
    position: absolute;
    top: 0;
    left: 0;
    height: 100vh;
    width: 100vw;
    filter: blur(1px);
    background: #191919;
   opacity: .99;
    z-index: 3;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-around;

    .popup-image{
      -webkit-animation: slide-in-top 1s cubic-bezier(0.250, 0.460, 0.450, 0.940) both;
	        animation: slide-in-top 1s cubic-bezier(0.250, 0.460, 0.450, 0.940) both;
    }
    .popup-paragraph{
      font-size: 4rem;
      font-weight: 700;
      letter-spacing: 3px;
      color: #FFFFFF;
      animation: shake .82s cubic-bezier(.36,.07,.19,.97) both;
      
    }
    .popup-button{
      outline: none;
      border: 2px #FEB800 dashed;
      border-radius: 2rem;
      background: transparent;
      color: #FEB800;
      width: 22rem;
      height: 5rem;
      font-size: 2rem;
    }
  }
  
  @keyframes shake {
  10%, 90% {
    transform: translate3d(-1px, 0, 0);
  }
  
  20%, 80% {
    transform: translate3d(2px, 0, 0);
  }

  30%, 50%, 70% {
    transform: translate3d(-4px, 0, 0);
  }

  40%, 60% {
    transform: translate3d(4px, 0, 0);
  }
}
@-webkit-keyframes slide-in-top {
  0% {
    -webkit-transform: translateY(-1000px);
            transform: translateY(-1000px);
    opacity: 0;
  }
  100% {
    -webkit-transform: translateY(0);
            transform: translateY(0);
    opacity: 1;
  }
}
@keyframes slide-in-top {
  0% {
    -webkit-transform: translateY(-1000px);
            transform: translateY(-1000px);
    opacity: 0;
  }
  100% {
    -webkit-transform: translateY(0);
            transform: translateY(0);
    opacity: 1;
  }
}

</style>