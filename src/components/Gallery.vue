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
            >
              <span v-if="isHovering" class="enlargement-icon">
                <i class="material-symbols-outlined">expand_content</i>
              </span>
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
                  @keyup.esc="closeEnlargedPhoto"
                  tabindex="0"
                  >
                </v-img>
            </div>
        </v-hover>
      </v-col>
    </v-row>
  </Suspense>
</template>

<script setup>
import { ref } from 'vue';

const { links } = defineProps(['links']);
console.log(links);
const selectedImage = ref(null);

const enlargePhoto = (elem) => {
  console.log("clicked on photo to open");
  selectedImage.value = elem;
  console.log(selectedImage.value);
}
const closeEnlargedPhoto = () => {
  console.log("clicked on photo to close");
  selectedImage.value = null;
}

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
    top: 0; /* these force the photo to only render once for reasons*/
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 2; /* Specify a stack order so that other pictures are not shown in the background */
    cursor: pointer; 
    display: flex; /* flexbox to center the pic vertically */
  }

  .enlargement-icon {
    display: flex;
    justify-content: center; 
    align-items: center; 
    position: absolute; 
    width: 100%;
    height: 100%;
  }

  .material-symbols-outlined {
    font-size: 100px; 
  }

</style>

