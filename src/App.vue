<script>
import { RouterLink, RouterView } from 'vue-router';
import Searchbar from './components/Searchbar.vue';
import axios from 'axios';
import Gallery from './components/Gallery.vue';


const key = import.meta.env.VITE_ACCESS_KEY;
const randomPhotoUrl = `https://api.unsplash.com/photos/random?client_id=${key}`;
const PhotoUrl = `https://api.unsplash.com/photos?client_id=${key}`;

export default {
  components: {
    Searchbar,
    Gallery
  },
  methods: {
    async getRandom() {
      try {
        const response = await axios.get(randomPhotoUrl);
        console.log(response);
      } catch (error) {
        console.log(error);
      }
    },
    async getSearchResults(searchTerms) {
      try {
        const searchPhotoUrl = `https://api.unsplash.com/search/photos?query=${searchTerms}&client_id=${key}`;
        const response = await axios.get(searchPhotoUrl);
        console.log(response);
      } catch (error) {
        console.log(error);
      }
    },
  }
}

</script>

<template>
  <div class="container">
    <nav class="navigation">
      <div>
        <RouterLink to="/">Home</RouterLink> <!-- HOME VIEW -->
      </div>
      <div>
        <RouterLink to="/feed">PicFeed</RouterLink> <!-- Gallery view -->
      </div>
    </nav>
    <div class="content-container">
      <div class="searchbar">
        <Searchbar @random="getRandom" @search="getSearchResults"/>
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
