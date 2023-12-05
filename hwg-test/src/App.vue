<script setup>
import { ref } from 'vue';
import Autocomplete from './components/autocomplete/Autocomplete.vue';
import PhotoGallery from './components/photo-gallery/PhotoGallery.vue';
import Carousel from './components/carousel/Carousel.vue';

import { images } from "./utiils/images"


const galleryData = ref(images);
</script>

<template>
  <div class="app-container">
    <Autocomplete :data="galleryData" />
    <PhotoGallery :data="galleryData" />
  </div>
  <Carousel :data="galleryData" />
</template>

<style>
.app-container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
</style>
