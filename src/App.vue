<script setup lang="ts">
import TipCalculator from "./components/Calculator.vue";
</script>

<template>
  <header>
    <h2>
      SPLITTER
    </h2>
  </header>
  <main>
    <TipCalculator />
  </main>

  <footer>
    <div class="attribution">
      Challenge by
      <a href="https://www.frontendmentor.io?ref=challenge" target="_blank">
        Frontend Mentor
      </a>.
      Coded by
      <a href="#">
        Your Name Here
      </a>.
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
      display: flex;
      justify-content: center;
      align-items: center;
    }
  </style>
