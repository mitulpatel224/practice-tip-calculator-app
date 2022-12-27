<script setup lang="ts">
import TheHeader from "./components/Header.vue";
import TipCalculator from "./components/Calculator.vue";
</script>

<template>
  <main>
    <TheHeader />
    <TipCalculator />
  </main>

  <footer>
    <div class="attribution">
      Challenge by
      <a href="https://www.frontendmentor.io?ref=challenge" target="_blank">
        Frontend Mentor </a
      >. Coded by <a href="#"> Your Name Here </a>.
    </div>
  </footer>
</template>

<style lang="scss">
@import "style.scss";

#app {
  height: 100%;
}

main {
  height: 100%;
  // display: flex;
  // flex-direction: column;
  // justify-content: center;
  // align-items: center;
}

@media (min-width: 1024px) {
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
}
</style>
