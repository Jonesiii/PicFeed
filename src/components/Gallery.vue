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
                <Maximize2 
                  :size="100"
                />
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
                  >
                  <X class="close-button" @click="closeEnlargedPhoto" @keyup.esc="closeEnlargedPhoto" :tabindex="0"
                    :size="40"
                    color="white"
                  />
                </v-img>
            </div>
        </v-hover>
      </v-col>
    </v-row>
  </Suspense>
</template>

<script setup>
import { ref } from 'vue';
import { Maximize2 } from 'lucide-vue-next'
import { X } from 'lucide-vue-next'

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
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 1); /* Black background with 90% opacity */
  z-index: 1000; /* Ensure it's on top of other elements */
}

.overlay .close-button {
  position: absolute;
  top: 20px;
  right: 20px;
  cursor: pointer;
  font-size: 24px;
}

.overlay img {
  max-width: 90%; /* Limit the image width */
  max-height: 90%; /* Limit the image height */
  object-fit: contain; /* Maintain image aspect ratio while fitting inside the container */
}

  .enlargement-icon {
    display: flex;
    justify-content: center; 
    align-items: center; 
    position: absolute; 
    width: 100%;
    height: 100%;
  }
</style>

