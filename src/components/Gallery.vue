<template> 
  <Suspense>
    <v-row>
      <v-col
        v-for="n in 9"
        :key="n"
        class="d-flex child-flex"
        cols="4"
      >
        <v-hover v-slot="{ isHovering, props }">
            <v-img
            :src="`https://picsum.photos/500/300?image=${n * 5 + 10}`"
            :lazy-src="`https://picsum.photos/10/6?image=${n * 5 + 10}`"
            :elevation="isHovering ? 12 : 2"
            :class="{ 'on-hover': isHovering }"
            @click="enlargePhoto"
            v-bind="props"
              aspect-ratio="1"
              cover
              class="bg-grey-lighten-2"
            >
              <template v-slot:placeholder>
                <v-row
                  class="fill-height ma-0"
                  align="center"
                  justify="center"
                >
                  <v-progress-circular
                    indeterminate
                    color="grey-lighten-5"
                  ></v-progress-circular>
                </v-row>
              </template>
            </v-img>
        </v-hover>
      </v-col>
    </v-row>
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
    //const response = await axios.get(PhotoUrl);
    //const data = Object.values(response.data);
    //links.value = data.map(item => item.urls.regular);
    console.log(links.value);
  } catch (error) {
    console.log(error);
  }
};

const enlargePhoto = () => {
  console.log("clicked on photo");
}

onMounted(() => {
  console.log(`the component is now mounted.`);
  getPhotoFeed();
});
</script>

<style scoped>
  .v-img {
    transition: opacity .4s ease-in-out;
  }

  .v-img:not(.on-hover) {
    opacity: 0.6;
  }

</style>

