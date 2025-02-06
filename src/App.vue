<script setup lang="ts">
import { reactive } from 'vue';

const state = reactive({
  operation: "+",
  valueOne: 0,
  valueTow: 0,
  result: 0
});

const changeOperator = (ev: Event) => {
  if (ev && ev.target) {
    state.operation = (<HTMLSelectElement>ev.target).value;
  }
}

const changeNumberOne = (ev: Event) => {
  if (ev && ev.target) {
    state.valueOne = parseFloat((<HTMLInputElement>ev.target).value);
  }
}

const changeNumberTow = (ev: Event) => {
  if (ev && ev.target) {
    state.valueTow = parseFloat((<HTMLInputElement>ev.target).value);
  }
}

const operations = () => {
  let { operation, valueOne, valueTow } = state;

  if ((valueOne != 0) && (valueTow != 0)) {
    switch (operation) {
      case "+":
        state.result = valueOne + valueTow;
        break;
      case "-":
        state.result = valueOne - valueTow;
        break;
      case "*":
        state.result = valueOne * valueTow;
        break;
      case "/":
        state.result = valueOne / valueTow;
        break;
      case "**":
        state.result = Math.pow(valueOne, valueTow);
        break;
      case "%":
        state.result = valueOne % valueTow;
        break;
      default:
        return;
    }
  }
}

</script>

<template>
  <main class="container d-flex flex-column align-items-center">

    <form class="form p-4 rounded-2 mt-5" @change="operations">
      <h1 class="mb-5 text-center">Calculadora</h1>

      <ul class="d-flex row list-unstyled row-gap-5 align-items-center justify-content-between">
        <li class="col-12 text-center form__result rounded-2">
          {{ state.result.toFixed(2) }}
        </li>

        <li class="col-12 p-0">
          <input type="number" name="" id="" class="form-control form__input" @change="changeNumberOne"
            placeholder="Primeiro número">
        </li>

        <li class="col-12 p-0">
          <input type="number" name="" id="" class="form-control form__input" @change="changeNumberTow"
            placeholder="Segundo número">
        </li>

        <li class="col-12 p-0">
          <select class="form-select" @change="changeOperator">
            <option selected value="+">Soma</option>
            <option value="-">Subtração</option>
            <option value="*">Multiplicação</option>
            <option value="/">Divisão</option>
            <option value="**">Potenciação</option>
            <option value="%">Resto da divisão</option>
          </select>
        </li>


      </ul>
    </form>
  </main>
</template>

<style scoped>
* {
  font-family: Roboto, sans-serif;
}

form {
  border: 1px solid #e9e9e9;
  background-color: #10db97;
  width: 300px;
}

h1 {
  color: #fff;
  text-transform: uppercase;
  font-size: 2rem;
}

.form__result {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100px;
  background-color: #dcfcce;
  font-size: 2rem;
  overflow: auto;
  font-family: Orbitron, sans-serif;
}

.form__span {
  padding: 0;
  font-size: 1.2rem;
}

.form__input {
  height: 50px;
  background-color: rgb(0, 179, 104);
  color: #fff;
  font-family: Silkscreen;
}

.form__input::placeholder {
  color: #fff;
}

select {
  background-color: rgb(0, 179, 104);
  color: #fff;
}
</style>
