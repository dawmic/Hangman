<script setup></script>
<template>
  <button class="gameBTn"><slot></slot></button>
</template>
<style lang="scss" scoped>
.gameBTn {
  outline: none;
  border: none;
  color: #feb800;
  width: 22rem;
  height: 5rem;
  font-size: 2rem;
  font-weight: 500;
  background: linear-gradient(90deg, #feb800 50%, transparent 0) repeat-x,
    linear-gradient(90deg, #feb800 50%, transparent 0) repeat-x,
    linear-gradient(0deg, #feb800 50%, transparent 0) repeat-y,
    linear-gradient(0deg, #feb800 50%, transparent 0) repeat-y;
  background-size: 6px 3px, 6px 3px, 3px 6px, 3px 6px;
  background-position: 0 0, 0 100%, 0 0, 100% 0;
  &:hover {
    animation: runningBorder 0.2s infinite linear;
  }
}

@keyframes runningBorder {
  100% {
    background-position: 6px 0, -6px 100%, 0 -6px, 100% 6px;
  }
}
</style>
