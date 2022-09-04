<script setup lang="ts">
import {} from "./BaseKey.vue";
import { reactive } from "vue";

interface themeControl {
  idx: number;
  curTheme: string;
  theme: { theme: string; position: string }[];
}

const themeSelector = reactive<themeControl>({
  idx: 0,
  curTheme: "theme-1",
  theme: [
    {
      theme: "theme-1",
      position: "flex-start",
    },
    {
      theme: "theme-2",
      position: "center",
    },
    {
      theme: "theme-3",
      position: "flex-end",
    },
  ],
});

function changeTheme(): void {
  const themeSelect = document.querySelector(".bar") as HTMLDivElement;
  if (themeSelector.idx === 2) {
    themeSelector.idx = 0;
    document.body.classList.remove(themeSelector.curTheme);
    document.body.classList.add("theme-1");
  } else themeSelector.idx++;

  themeSelect.style.justifyContent =
    themeSelector.theme[themeSelector.idx].position;
  document.body.classList.remove(themeSelector.curTheme);
  themeSelector.curTheme = themeSelector.theme[themeSelector.idx].theme;

  document.body.classList.add(themeSelector.curTheme);
}
</script>

<template>
  <div class="theme-control">
    <h2 class="uppercase">theme</h2>
    <div class="theme--panel">
      <div class="number">
        <span>1</span>
        <span>2</span>
        <span>3</span>
      </div>
      <div class="bar">
        <div @click="changeTheme"></div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.theme-control {
  @include flex(2rem);
  align-items: flex-end;

  h2 {
    margin-bottom: 0.1rem;
    font-size: 12px;
    letter-spacing: 1.75px;
    color: var(--text-header);
    text-transform: uppercase;
  }

  .theme--panel {
    width: 80px;

    .number {
      @include flex(0.5rem);
      @include fontSize($fs-200);
      justify-content: space-between;
      padding-inline: 0.5rem;

      span {
        color: var(--text-header);
        @include desktop {
          font-size: 16px;
        }
      }
    }
  }
}
.bar {
  @include flex(0);
  width: 100%;
  border-radius: 24px;
  align-items: center;
  padding: 5px 5px;
  background-color: var(--keypad-bg);

  & > * {
    width: 16px;
    height: 16px;
    border-radius: 50%;
    background-color: var(--bg-key-3);
    cursor: pointer;
  }
}
</style>
