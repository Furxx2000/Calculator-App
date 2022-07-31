<script setup lang="ts">
import {} from "./TheDisplayWindow.vue";

const emit = defineEmits(["get-key"]);

function keyClick(e: MouseEvent) {
  const target = e.target as HTMLElement;
  const buttonEl =
    target.tagName.toLowerCase() === "button" ? target : target.parentElement!;
  const action = buttonEl?.textContent;
  const btnContainer = buttonEl.closest("section");

  if (
    target.tagName.toLowerCase() !== "button" &&
    target.tagName.toLowerCase() !== "p"
  )
    return;

  if (action === "+" || action === "-" || action === "x" || action === "/") {
    btnContainer
      ?.querySelector("[aria-selected='true']")
      ?.setAttribute("aria-selected", "false");
    buttonEl.setAttribute("aria-selected", "true");
  } else {
    btnContainer
      ?.querySelector("[aria-selected='true']")
      ?.setAttribute("aria-selected", "false");
  }

  emit("get-key", action);
}
</script>

<template>
  <section @click="keyClick">
    <button class="seven" aria-selected="false">
      <p>7</p>
    </button>
    <button class="eight" aria-selected="false">
      <p>8</p>
    </button>
    <button class="nine" aria-selected="false">
      <p>9</p>
    </button>
    <button class="delete uppercase">
      <p>del</p>
    </button>
    <button class="four" aria-selected="false">
      <p>4</p>
    </button>
    <button class="five" aria-selected="false">
      <p>5</p>
    </button>
    <button class="six" aria-selected="false">
      <p>6</p>
    </button>
    <button class="plus" aria-selected="false">
      <p>+</p>
    </button>
    <button class="one" aria-selected="false">
      <p>1</p>
    </button>
    <button class="two" aria-selected="false">
      <p>2</p>
    </button>
    <button class="three" aria-selected="false">
      <p>3</p>
    </button>
    <button class="minus" aria-selected="false">
      <p>-</p>
    </button>
    <button class="dot" aria-selected="false">
      <p>.</p>
    </button>
    <button class="zero" aria-selected="false">
      <p>0</p>
    </button>
    <button class="slash" aria-selected="false">
      <p>/</p>
    </button>
    <button class="multiply" aria-selected="false">
      <p>x</p>
    </button>
    <button class="reset uppercase" aria-selected="false">
      <p>reset</p>
    </button>
    <button class="equal" aria-selected="false">
      <p>=</p>
    </button>
  </section>
</template>

<style lang="scss" scoped>
section {
  width: 100%;
  @include container(1.5rem, 1.5rem, 100%);
  @include grid(0.8rem);
  @include desktop {
    @include container(2rem, 2rem, 100%);
    @include grid(1.5rem);
    row-gap: 2rem;
  }
  row-gap: 1.1rem;
  grid-template-areas:
    "seven eight nine delete" "four five six plus"
    "one two three minus" "dot zero slash multiply" "reset reset equal equal";
  background-color: var(--keypad-bg);
  border-radius: 8px;
}

button {
  position: relative;
  appearance: none;
  display: block;
  font-size: $fs;
  border: none;
  border-radius: 6px;
  transition: all 0.05s ease-in;
  @include grid(0);
  cursor: pointer;
}

button:active {
  transform: translateY(4px);
  box-shadow: none;
}

button[aria-selected="true"] {
  transform: translateY(4px);
  box-shadow: none;
  background-color: var(--bg-key-1-shadow);
}

section > button > p {
  position: absolute;
  place-self: center;
  padding-top: 6px;
}

.seven {
  @include keyType-1(seven);
}

.eight {
  @include keyType-1(eight);
}

.nine {
  @include keyType-1(nine);
}

.delete {
  @include keyType-2(delete);
  font-size: 20px;
}

.four {
  @include keyType-1(four);
}

.five {
  @include keyType-1(five);
}

.six {
  @include keyType-1(six);
}

.plus {
  @include keyType-1(plus);
}

.one {
  @include keyType-1(one);
}

.two {
  @include keyType-1(two);
}

.three {
  @include keyType-1(three);
}

.minus {
  @include keyType-1(minus);
}

.dot {
  @include keyType-1(dot);
}

.zero {
  @include keyType-1(zero);
}

.slash {
  @include keyType-1(slash);
}

.multiply {
  @include keyType-1(multiply);
}

.reset {
  @include keyType-2(reset);
  font-size: 20px;
}

.equal {
  @include keyType-3(equal);
  font-size: 1.2rem;
}
</style>
