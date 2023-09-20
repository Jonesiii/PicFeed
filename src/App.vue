<script setup>
import { ref, onMounted, onBeforeUnmount, computed } from 'vue';
import axios from 'axios';
import Searchbar from './components/Searchbar.vue';
import Gallery from './components/Gallery.vue';
import RandomButton from './components/RandomButton.vue';
import FeedButton from './components/FeedButton.vue';

const key = import.meta.env.VITE_ACCESS_KEY;
const randomPhotoUrl = `https://api.unsplash.com/photos/random?client_id=${key}`;
const photoUrl = `https://api.unsplash.com/photos?client_id=${key}`;

const isSearching = ref(false);
const searchResults = ref([]);
const feedLinks = ref([]);
const screenWidth = ref(window.innerWidth);

const displayedLinks = computed(() => {
  if (isSearching.value) {
    return searchResults.value;
  } else {
    return feedLinks.value;
  }
});

const getRandom = async () => {
  try {
    stopSearching();
    feedLinks.value = [];
    const response = await axios.get(randomPhotoUrl);
    const data = Object.values(response.data);
    feedLinks.value = [data[12].regular];
  } catch (error) {
    console.log(error);
  }
};

const getSearchResults = async (searchTerms) => {
  try {
    isSearching.value = true;
    const searchPhotoUrl = `https://api.unsplash.com/search/photos?query=${searchTerms}&client_id=${key}`;
    const response = await axios.get(searchPhotoUrl);
    const data = Object.values(response.data);
    searchResults.value = data[2].map(item => item.urls.regular);
  } catch (error) {
    console.log(error);
  }
};

const getPhotoFeed = async () => {
  try {
    stopSearching();
    feedLinks.value = [];
    const response = await axios.get(photoUrl);
    const data = Object.values(response.data);
    feedLinks.value = data.map(item => item.urls.regular);
  } catch (error) {
    console.log(error);
  }
};

const stopSearching = () => {
  isSearching.value = false;
};

const updateScreenWidth = () => {
  screenWidth.value = window.innerWidth;
};

onMounted(()=> {
  getPhotoFeed();
  window.addEventListener("resize", updateScreenWidth);
});

onBeforeUnmount(() => {
  window.removeEventListener("resize", updateScreenWidth);
})

</script>


<template>
  <div class="container">
    <div class="content-container">
      <div v-if="screenWidth > 768" class="searchbar-and-nav">
        <FeedButton @getFeed="getPhotoFeed"/>
        <Searchbar @search="getSearchResults"/>
        <RandomButton @random="getRandom" />
      </div>
      <div v-else class="searchbar-and-nav-narrow">
        <div>
          <Searchbar class="searchbox" @search="getSearchResults"/>
        </div>
        <div class="buttons">
          <FeedButton @getFeed="getPhotoFeed"/>
          <RandomButton @random="getRandom" />
        </div>
      </div>
      <div class="content">
        <div class="content">
        <Gallery :links="displayedLinks" />
      </div>
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

.searchbar-and-nav-narrow {
  display: flex;
  flex-direction: column; /* Stack elements vertically */
  align-items: center; /* Center horizontally */
  justify-content: center; /* Center vertically */
  text-align: center; /* Center text or inline elements */
}

.buttons {
  margin-top:3%;
}

.buttons > *:first-child {
  padding: 20px;
  right:20%;
}
.buttons > *:last-child {
  padding: 20px;
  left:10%;
}

.searchbox {
  margin-top:25%;
}
</style>
