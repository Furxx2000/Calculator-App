<template>
  <main class="calculator">
    <TheHeader />
    <TheDisplayWindow :calcVal="calcState.curVal" />
    <TheKeypad @handle-calculate="calculator" />
  </main>
</template>

<script setup lang="ts">
import { reactive } from 'vue';

interface CalcType {
  curVal: string;
  operator: string;
  totalNumber: number;
  operators: string;
  clearDisplay: boolean;
}

const calcState = reactive<CalcType>({
  curVal: '',
  operator: '',
  totalNumber: 0,
  operators: '+-x/=',
  clearDisplay: false,
});

function addNumber() {
  calcState.curVal = (calcState.totalNumber + +calcState.curVal).toString();
}

function subtractNumber() {
  calcState.curVal = (calcState.totalNumber - +calcState.curVal).toString();
}

function multiplyNumber() {
  calcState.curVal = (calcState.totalNumber * +calcState.curVal).toString();
}

function divideNumber() {
  if (calcState.totalNumber / +calcState.curVal < 1) {
    calcState.curVal = (calcState.totalNumber / +calcState.curVal)
      .toFixed(4)
      .toString();
  } else {
    calcState.curVal = (calcState.totalNumber / +calcState.curVal).toString();
  }
}

function deleteNumber() {
  if (!calcState.curVal) {
    resetCalcState();
    return;
  }
  calcState.curVal = '';
}

function resetCalcState() {
  calcState.curVal = '';
  calcState.operator = '';
  calcState.totalNumber = 0;
  calcState.clearDisplay = false;
}

function checkZeroAndComma(key: string) {
  let isValid = true;

  if (calcState.curVal === '0' && key !== '.') {
    isValid = false;
    return isValid;
  }

  if (calcState.curVal.includes('.') && key === '.') {
    isValid = false;
    return isValid;
  }

  if (calcState.curVal.length >= 10) {
    isValid = false;
    return isValid;
  }

  return isValid;
}

function executeOperator(key: string) {
  if (calcState.totalNumber) {
    if (calcState.operator === '+') addNumber();
    if (calcState.operator === '-') subtractNumber();
    if (calcState.operator === 'x') multiplyNumber();
    if (calcState.operator === '/') divideNumber();
    calcState.totalNumber = 0;
  }

  calcState.operator = key;
  calcState.clearDisplay = true;
}

function showDisplayNumber(key: string) {
  if (calcState.clearDisplay) {
    calcState.totalNumber = +calcState.curVal;
    calcState.curVal = key;
    calcState.clearDisplay = false;
  } else {
    if (!calcState.curVal && key === '.') calcState.curVal += '0.';
    else calcState.curVal += key;
  }
}

function calculator(key: string) {
  if (key === 'del') deleteNumber();
  if (key === 'reset') resetCalcState();
  if (!checkZeroAndComma(key)) return;

  if (calcState.operators.includes(key)) executeOperator(key);
  if (key === '.' || !isNaN(+key)) showDisplayNumber(key);
}
</script>

<style lang="scss" scoped>
.calculator {
  margin: 0 auto;
  grid-template-rows: 1fr 2fr 9fr;
  @include container(0, 1.5rem, 40rem);
  @include grid(1.5rem);
  @include desktop {
    @include container(12vh, 1.5rem, 35rem);
  }
}
</style>
