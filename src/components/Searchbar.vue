

<template>
  <div>
    <input class="searchbar" type="text" placeholder="Search for pics..." @keyup.enter="emitSearch" v-model="query" />
    <button @click.prevent="emitSearch" >Search</button>
  </div>
  
  <button class="randomButton" @click.prevent="emitRandom">Random</button>
</template>

<script setup>
import { ref, defineEmits } from 'vue';

const query = ref("");
const emits = defineEmits(['random', 'search']);

const resetSearchField = () => {
  query.value = '';
};

const emitRandom = () => {
  console.log('clicked');
  emits('random');
};

const emitSearch = () => {
  console.log(`searched with ${query.value}`);
  emits('search', query.value);
  resetSearchField();
};
</script>
