<template> 
  <Suspense>
    <div>
      <h3>
        Gallery here
      </h3>
      <ul>
        <li v-for="link in links" :key="link">
          <img :src="link" alt="">
        </li>
      </ul>
    </div>
  </Suspense>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const key = import.meta.env.VITE_ACCESS_KEY;
const PhotoUrl = `https://api.unsplash.com/photos?client_id=${key}`;

const links = ref([]);
const getPhotoFeed = async () => {
  try {
    console.log("sent feedreq");
    const response = await axios.get(PhotoUrl);
    const data = Object.values(response.data);
    links.value = data.map(item => item.urls.regular);
    console.log(links.value);
  } catch (error) {
    console.log(error);
  }
};

onMounted(() => {
  console.log(`the component is now mounted.`);
  getPhotoFeed();
});
</script>
