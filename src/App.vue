<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Searchbar from './components/Searchbar.vue';

</script>

<template>
  <div class="container">
    <nav class="navigation">
      <RouterLink to="/">Home</RouterLink>
    </nav>
    <div class="content-container">
      <div class="searchbar">
        <Searchbar />
      </div>
      <div class="content">
        <RouterView />
      </div>
    </div>
  </div>
  
</template>

<style scoped>
.container {
  background-color: #1c1b17;
  display: flex;
  height: 100vh;
}

.navigation {
  flex-basis: 10%;
  background-color: lightgray;
  padding: 20px;
  box-sizing: border-box;
}

.content-container {
  display: flex;
  flex-direction: column;
  flex: 1;
}
.content {
  flex-basis: 90%;
  background-color: #1c1b17;
  color: aquamarine;
  padding: 20px;
  box-sizing: border-box;
  margin: auto;
}

.searchbar {
  margin: auto;
}
</style>
