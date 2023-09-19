<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import Searchbar from './components/Searchbar.vue';
import Gallery from './components/Gallery.vue';
import RandomButton from './components/RandomButton.vue';
import FeedButton from './components/FeedButton.vue';

const key = import.meta.env.VITE_ACCESS_KEY;
const randomPhotoUrl = `https://api.unsplash.com/photos/random?client_id=${key}`;
const photoUrl = `https://api.unsplash.com/photos?client_id=${key}`;

const isSearching = ref(false);
const onRandomPage = ref(false);
const searchResults = ref([]);
const feedLinks =ref([]);

const getRandom = async () => {
  try {
    stopSearching();
    feedLinks.value = [];
    const response = await axios.get(randomPhotoUrl);
    console.log(response);
    feedLinks.value = [response.data.urls.regular];
  } catch (error) {
    console.log(error);
  }
};

const getSearchResults = async (searchTerms) => {
  try {
    isSearching.value = true;
    const searchPhotoUrl = `https://api.unsplash.com/search/photos?query=${searchTerms}&client_id=${key}`;
    const response = await axios.get(searchPhotoUrl);
    console.log(response);
    const data = Object.values(response.data);
    console.log(data);
    searchResults.value = data[2].map(item => item.urls.regular);
  } catch (error) {
    console.log(error);
  }
};

const getPhotoFeed = async () => {
  try {
    stopSearching();
    console.log("sent feedreq");
    const response = await axios.get(photoUrl);
    const data = Object.values(response.data);
    feedLinks.value = data.map(item => item.urls.regular);
    console.log(feedLinks.value);
  } catch (error) {
    console.log(error);
  }
};

onMounted(()=> {
  getPhotoFeed();
});

const stopSearching = () => {
  isSearching.value = false;
};

</script>


<template>
  <div class="container">
    <div class="content-container">
      <div class="searchbar-and-nav">
        <FeedButton @getFeed="getPhotoFeed"/>
        <Searchbar @search="getSearchResults"/>
        <RandomButton @random="getRandom" />
      </div>
      <div class="content">
        <Gallery v-if="!isSearching && feedLinks.length > 0" :links="feedLinks" />
        <Gallery v-if="isSearching && searchResults.length > 0" :links="searchResults" />
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
  flex: 1;
  background-color: #1c1b17;
  color: white;
  padding: 25px;
}

.searchbar-and-nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  }

.searchbar-and-nav > *:first-child {
  margin-left: auto; 
  padding: 20px;
  top:15%;
  right:3%;
}

.searchbar-and-nav > *:last-child {
  margin-right: auto; 
  padding: 20px;
  top:15%;
  left:3%;
}
.searchbar-and-nav > *:nth-child(2) {
  top:15%;
}
</style>
