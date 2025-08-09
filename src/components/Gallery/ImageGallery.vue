<template>
  <div class="w-full max-w-6xl">
    <h2 class="text-3xl font-bold text-center mb-8">Gallery</h2>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
      <div 
        v-for="(image, index) in images" 
        :key="index"
        class="aspect-square overflow-hidden rounded-lg cursor-pointer group"
        @click="openLightbox(index)"
      >
        <img 
          :src="image" 
          :alt="`Gallery image ${index + 1}`"
          class="w-full h-full object-cover hover:scale-105 transition-transform duration-300 group-hover:brightness-110"
        />
      </div>
    </div>

    <!-- Lightbox Component -->
    <Lightbox 
      :images="images"
      :is-visible="showLightbox"
      :initial-index="lightboxIndex"
      @close="closeLightbox"
    />
  </div>
</template>

<script>
import Lightbox from '../Lightbox.vue';

export default {
  components: {
    Lightbox
  },
  props: {
    images: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      showLightbox: false,
      lightboxIndex: 0
    }
  },
  methods: {
    openLightbox(index) {
      this.lightboxIndex = index;
      this.showLightbox = true;
    },
    closeLightbox() {
      this.showLightbox = false;
    }
  }
}
</script>
