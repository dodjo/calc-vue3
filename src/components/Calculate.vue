<template>
<div class="calculate">
  <input class="calculate__display" type="text" v-model="display" disabled>
  <div class="buttons">
    <UiButton v-for="button in buttons"
            :key="button.value"
            :class="button.type"
            @click="handleClick(button.value)">
      {{ button.value }}
    </UiButton>
  </div>
</div>
</template>

<script setup>
import {ref} from "vue";
import UiButton from "./UiButton.vue";

const display = ref('')
const buttons = [
  {value: 'AC', type: 'clear'},
  {value: 'DEL', type: 'delete'},
  {value: '.', type: 'operator'},
  {value: '/', type: 'operator'},

  {value: '7'},
  {value: '8'},
  {value: '9'},
  {value: '*', type: 'operator'},

  {value: '4'},
  {value: '5'},
  {value: '6'},
  {value: '-', type: 'operator'},

  {value: '1'},
  {value: '2'},
  {value: '3'},
  {value: '+', type: 'operator'},

  {value: '000'},
  {value: '00'},
  {value: '0'},
  {value: '=', type: 'equals'},
]

const handleClick = (value) => {
  if (value === 'AC') {
    return display.value = ''
  }

  if (value === 'DEL') {
    return display.value = display.value.slice(0, -1)
  }

  if (value === '=') {
    return display.value = eval(display.value)
  }

  display.value += value
}
</script>

<style lang="scss" scoped>
.calculate {
  padding: 2rem;
  border-radius: 8px;
  border: 1px solid gray;
  display: flex;
  flex-direction: column;
  gap: 0.8rem;

  &__display {
    padding: 1.5rem 1rem;
    text-align: right;
    font-size: 2rem;
    background-color: #1a1a1a;
    color: #ffffff;
    border: none;
    border-radius: 8px;
  }

}
.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 0.8rem;
}
</style>
