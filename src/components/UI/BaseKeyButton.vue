<script setup lang="ts">
import { toRefs } from '@vue/reactivity';

interface Props {
  name: string;
  text: string;
  isSelected: boolean;
}

const props = defineProps<Props>();
const { name, text, isSelected } = toRefs(props);
</script>

<template>
  <button :class="name" :aria-selected="isSelected" role="tab" tabindex="-1">
    <span>{{ text }}</span>
  </button>
</template>

<style lang="scss" scoped>
button {
  position: relative;
  appearance: none;
  border: none;
  border-radius: 6px;
  font-size: $fs;
  transition: all 0.05s ease-in;
  cursor: pointer;
  @include grid(0);
  @include desktop {
    border-radius: 10px;
    font-size: 36px;
  }
}

button:active {
  transform: translateY(4px);
  box-shadow: none;
}

button[aria-selected='true'] {
  transform: translateY(4px);
  box-shadow: none;
  background-color: var(--bg-key-1-shadow);
}

button > span {
  position: absolute;
  place-self: center;
  padding-top: 6px;
}
</style>
