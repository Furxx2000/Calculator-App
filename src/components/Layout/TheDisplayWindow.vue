<script setup lang="ts">
import { toRefs } from '@vue/reactivity';
import { computed } from 'vue';

interface Props {
  calcVal: string;
}

const props = defineProps<Props>();
const { calcVal } = toRefs(props);

const val = computed(() => {
  if (calcVal.value === '') {
    return '0';
  } else {
    return calcVal.value.replace(/\B(?=(\d{3})+(?!\d))/g, ',');
  }
});
</script>

<template>
  <div id="display" class="display-window">{{ val }}</div>
</template>

<style lang="scss" scoped>
.display-window {
  display: grid;
  align-items: center;
  appearance: none;
  outline: none;
  width: 100%;
  color: var(--text-header);
  padding-inline: 1.6rem;
  padding-top: 0.5rem;
  font: inherit;
  font-size: 40px;
  border: 0;
  border-radius: 8px;
  background-color: var(--screen-bg);
  text-align: right;
  @include desktop {
    font-size: 48px;
  }
}
</style>
