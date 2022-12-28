<script setup lang="ts">
import {} from './TheDisplayWindow.vue';

const emit = defineEmits(['get-key']);

const keysData = [
  {
    name: 'zero',
    text: '0',
    isSelected: false,
  },
  {
    name: 'one',
    text: '1',
    isSelected: false,
  },
  {
    name: 'two',
    text: '2',
    isSelected: false,
  },
  {
    name: 'three',
    text: '3',
    isSelected: false,
  },
  {
    name: 'four',
    text: '4',
    isSelected: false,
  },
  {
    name: 'five',
    text: '5',
    isSelected: false,
  },
  {
    name: 'six',
    text: '6',
    isSelected: false,
  },
  {
    name: 'seven',
    text: '7',
    isSelected: false,
  },
  {
    name: 'eight',
    text: '8',
    isSelected: false,
  },
  {
    name: 'nine',
    text: '9',
    isSelected: false,
  },
  {
    name: 'dot',
    text: '.',
    isSelected: false,
  },
  {
    name: 'plus',
    text: '+',
    isSelected: false,
  },
  {
    name: 'minus',
    text: '-',
    isSelected: false,
  },
  {
    name: 'multiply',
    text: 'x',
    isSelected: false,
  },
  {
    name: 'slash',
    text: '/',
    isSelected: false,
  },
  {
    name: 'delete',
    text: 'del',
    isSelected: false,
  },
  {
    name: 'reset',
    text: 'reset',
    isSelected: false,
  },
  {
    name: 'equal',
    text: '=',
    isSelected: false,
  },
];

function keyClick(e: MouseEvent) {
  const target = e.target as HTMLElement;
  const buttonEl =
    target.tagName.toLowerCase() === 'button' ? target : target.parentElement!;
  const action = buttonEl?.textContent;
  const btnContainer = buttonEl.closest('.keypad');

  if (
    target.tagName.toLowerCase() !== 'button' &&
    target.tagName.toLowerCase() !== 'span'
  )
    return;

  if (action === '+' || action === '-' || action === 'x' || action === '/') {
    btnContainer
      ?.querySelector("[aria-selected='true']")
      ?.setAttribute('aria-selected', 'false');
    buttonEl.setAttribute('aria-selected', 'true');
  } else {
    btnContainer
      ?.querySelector("[aria-selected='true']")
      ?.setAttribute('aria-selected', 'false');
  }

  emit('get-key', action);
}
</script>

<template>
  <div class="keypad" @click="keyClick" role="tablist">
    <BaseKeyButton
      v-for="key in keysData"
      :key="key.name"
      :name="key.name"
      :text="key.text"
      :is-selected="key.isSelected"
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
    'seven eight nine delete' 'four five six plus'
    'one two three minus' 'dot zero slash multiply' 'reset reset equal equal';

  @include container(1.5rem, 1.5rem, 100%);
  @include grid(0.8rem);
  @include desktop {
    @include container(2rem, 2rem, 100%);
    @include grid(1.5rem);
    row-gap: 2rem;
  }
}

$keys1: zero, one, two, three, four, five, six, seven, eight, nine, dot, slash,
  multiply, minus, plus;

$keys2: delete, reset;

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

.equal {
  font-size: 1.2rem;
  @include keyType-3(equal);
  @include desktop {
    font-size: 24px;
  }
}
</style>
