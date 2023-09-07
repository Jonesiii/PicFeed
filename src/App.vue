<script>
import { RouterLink, RouterView } from 'vue-router';
import Searchbar from './components/Searchbar.vue';
import axios from 'axios';


const key = import.meta.env.VITE_ACCESS_KEY;
const randomPhotoUrl = `https://api.unsplash.com/photos/random?client_id=${key}`
const random = 'https://api.unsplash.com/photos/random'

export default {
  components: {
    Searchbar
  },
  methods: {
    async getRandom() {
      console.log("got here", key);
      try {
        console.log("working");
        const response = await axios.get(randomPhotoUrl);
        console.log(response);
      } catch (error) {
        console.log(error);
      }
    }
  }
}

</script>

<template>
  <div class="container">
    <nav class="navigation">
      <RouterLink to="/">Home</RouterLink>
    </nav>
    <div class="content-container">
      <div class="searchbar">
        <Searchbar @random="getRandom"/>
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
