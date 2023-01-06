<script setup>
import {ref, computed} from 'vue';
const name = 'Vue dinámico';

const counter = ref(0);
const arrayFavoritos = ref([]);

// Método- methods
const increment = () => {
  counter.value++;
}

const decrease = () => {
  counter.value--;
}

const reset = () => {
  counter.value = 0
}

const add = () => {
  arrayFavoritos.value.push(counter.value);
}

const bloquearBtnAdd = computed(() => {
  const numSearch = arrayFavoritos.value.find(num => num === counter.value)
  console.log(numSearch);
  if(numSearch === 0) return true;
  return numSearch ? true : false;
})

const classCounter = computed(() => {
  if(counter.value === 0) {
    return 'zero'
  }
  if(counter.value > 0){
    return 'positive'
  }
  if(counter.value < 0){
    return 'negative'
  }
})

</script>

<template>
  <div class="container text-center mt-3">
    <h1>Qué sucede {{ name.toUpperCase() }}?</h1>
    <h2 :class="classCounter">{{ counter }}</h2>
    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Increment</button>
      <button @click="decrease" class="btn btn-danger">Decrease</button>
      <button @click="reset" class="btn btn-secondary">Reset</button>
      <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">Add</button>
    </div>
    <ul class="list-group mt-3">
      <li v-for="(num, index) in arrayFavoritos" :key="index" class="list-group-item">
        {{ num }}
      </li>
    </ul>
  </div>

</template>

<style>
  h1{
    color: rgb(236, 2, 2);
  }
  .positive{
    color: green;
  }
  .negative{
    color: red;
  }
  .zero{
    color: rgb(74, 57, 39);
  }
</style>