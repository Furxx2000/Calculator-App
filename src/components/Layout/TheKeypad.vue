<script setup lang="ts">
import { ref } from '@vue/runtime-core';
import { keysData } from '../../helpers/keys';

interface Key {
  name: string;
  text: string;
  isSelected?: boolean;
}

const emit = defineEmits(['handleCalculate']);
const refKeys = ref(keysData);

function handleKeyClick(key: string) {
  const operators = '+-x/';

  if (operators.includes(key)) {
    const newArr = refKeys.value.map((k: Key) => {
      return {
        ...k,
        isSelected: k.text === key,
      };
    });
    refKeys.value = newArr;
  } else {
    refKeys.value = keysData;
  }

  emit('handleCalculate', key);
}
</script>

<template>
  <div class="keypad">
    <BaseKeyButton
      v-for="key in refKeys"
      :key="key.name"
      :name="key.name"
      :text="key.text"
      :is-selected="key.isSelected"
      :handleKeyClick="handleKeyClick"
    />
  </div>
</template>

<style lang="scss" scoped>
.keypad {
  width: 100%;
  row-gap: 1.1rem;
  border-radius: 8px;
  background-color: var(--keypad-bg);
  grid-template-areas:
    'seven eight nine clear' 'four five six add'
    'one two three subtract' 'decimal zero divide multiply' 'reset reset equals equals';

  @include container(1.5rem, 1.5rem, 100%);
  @include grid(0.8rem);
  @include desktop {
    @include container(2rem, 2rem, 100%);
    @include grid(1.5rem);
    row-gap: 2rem;
  }
}

$keys1: zero, one, two, three, four, five, six, seven, eight, nine, decimal,
  divide, multiply, subtract, add;

$keys2: clear, reset;

@each $key in $keys1 {
  .#{$key} {
    @include keyType-1($key);
  }
}

@each $key in $keys2 {
  .#{$key} {
    font-size: 20px;
    text-transform: uppercase;
    @include keyType-2($key);
    @include desktop {
      font-size: 28px;
    }
  }
}

.equals {
  font-size: 1.2rem;
  @include keyType-3(equals);
  @include desktop {
    font-size: 24px;
  }
}
</style>
