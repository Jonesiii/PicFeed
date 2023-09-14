<template> 
  <Suspense>
    <v-row>
      <v-col
        v-for="link in links"
        :key="link"
        class="d-flex child-flex"
        cols="4"
      >
        <v-hover v-slot="{ isHovering, props }" >
          <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200" />
            <v-img
            :src="link"
            :elevation="isHovering ? 12 : 2"
            :class="{ 'on-hover': isHovering }"
            @click="enlargePhoto(link)"
            v-bind="props"
              aspect-ratio="1"
              cover
              class="bg-grey-lighten-2"
            >
            <span v-if="isHovering" class="material-symbols-outlined">expand_content</span>
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
            <div v-if="selectedImage" class="overlay">
              <v-img
                :src="selectedImage"
                @click="closeEnlargedPhoto"
              >
              </v-img>
            </div>
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
const selectedImage = ref(null);

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

const enlargePhoto = (elem) => {
  console.log("clicked on photo to open");
  selectedImage.value = elem;
}
const closeEnlargedPhoto = () => {
  console.log("clicked on photo to close");
  selectedImage.value = null;
}

onMounted(() => {
  console.log(`the component is now mounted.`);
  getPhotoFeed();
});
</script>

<style scoped>

@import url("https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200");
  .v-img {
    transition: opacity .4s ease-in-out;
  }

  .v-img:not(.on-hover) {
    opacity: 0.6;
  }
  .v-img.on-hover {
    cursor: pointer;
  }

  .overlay {
  position: fixed; /* Sit on top of the page content */
  width: 100%; /* Full width (cover the whole page) */
  height: 100%; /* Full height (cover the whole page) */
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 2; /* Specify a stack order in case you're using a different order for other elements */
  cursor: pointer; /* Add a pointer on hover */
  }

  .material-symbols-outlined {
    position:auto;
    width: 100%;
    height: 100%;
  }

</style>

