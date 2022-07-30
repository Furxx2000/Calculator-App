<template>
  <MainCalculator />
</template>

<script setup lang="ts">
import { onBeforeMount } from "@vue/runtime-core";

onBeforeMount(() => {
  document.body.classList.add("theme-1");
});
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=League+Spartan:wght@700&display=swap");

*,
*::before,
*::after {
  box-sizing: border-box;
}

body {
  line-height: 1.5;
  height: 100vh;
  font-family: "League Spartan", sans-serif;
  background-color: var(--main-bg);
  margin: 0;
}
</style>
