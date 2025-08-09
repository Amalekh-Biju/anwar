<template>
  <div class="w-full h-screen relative overflow-hidden">
    <!-- Image carousel -->
    <div 
      class="flex transition-transform duration-500 ease-in-out h-full"
      :style="{ transform: `translateX(-${currentSlide * 100}%)` }"
    >
      <div 
        v-for="(image, index) in images" 
        :key="index"
        class="w-full h-full flex-shrink-0 relative cursor-pointer"
        @click="openLightbox(index)"
      >
        <img 
          :src="image" 
          :alt="`Nirmala Mansion ${index + 1}`"
          class="w-full h-full object-cover cursor-pointer"
        @click="openLightbox(currentSlide)"
        />
        <div class="absolute inset-0 bg-gradient-to-b from-black/30 to-black/60"></div>
      </div>
    </div>

    <!-- Content overlay -->
    <div class="absolute inset-0 z-20 flex items-center justify-center">
      <div class="text-center text-white px-4 max-w-4xl">
        <h1 class="text-4xl lg:text-7xl font-bold mb-6">{{ card.title }}</h1>
        <p class="text-xl lg:text-3xl mb-8 prata">{{ card.tagline }}</p>
        <div class="flex flex-wrap justify-center gap-4 mb-8">
          <span 
            v-for="highlight in card.highlights" 
            :key="highlight"
            class="bg-white/20 backdrop-blur-sm px-4 py-2 rounded-full text-sm font-medium"
          >
            {{ highlight }}
          </span>
        </div>
        <div class="flex flex-col sm:flex-row gap-4 justify-center">
          <a 
            href="#contact" 
            class="bg-green-600 hover:bg-green-700 text-white px-8 py-3 rounded-lg font-medium transition-colors"
          >
            Contact Us
          </a>
          <a 
            href="#amenities" 
            class="border-2 border-white text-white hover:bg-white hover:text-gray-900 px-8 py-3 rounded-lg font-medium transition-colors"
          >
            View Amenities
          </a>
        </div>
      </div>
    </div>

    <!-- Navigation arrows -->
    <button 
      @click="prevSlide"
      class="absolute left-4 top-1/2 transform -translate-y-1/2 z-30 bg-black/50 hover:bg-black/70 text-white p-3 rounded-full transition-colors"
      v-if="images.length > 1"
    >
      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <path d="m15 18-6-6 6-6"/>
      </svg>
    </button>
    
    <button 
      @click="nextSlide"
      class="absolute right-4 top-1/2 transform -translate-y-1/2 z-30 bg-black/50 hover:bg-black/70 text-white p-3 rounded-full transition-colors"
      v-if="images.length > 1"
    >
      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <path d="m9 18 6-6-6-6"/>
      </svg>
    </button>

    <!-- Dots indicator -->
    <div class="absolute bottom-8 left-1/2 transform -translate-x-1/2 z-30 flex gap-2" v-if="images.length > 1">
      <button 
        v-for="(image, index) in images" 
        :key="index"
        @click="currentSlide = index"
        class="w-3 h-3 rounded-full transition-colors"
        :class="currentSlide === index ? 'bg-white' : 'bg-white/50'"
      />
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
import Lightbox from './Lightbox.vue';

export default {
  components: {
    Lightbox
  },
  props: {
    images: {
      type: Array,
      required: true
    },
    card: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      currentSlide: 0,
      autoSlideInterval: null,
      showLightbox: false,
      lightboxIndex: 0
    }
  },
  methods: {
    nextSlide() {
      this.currentSlide = (this.currentSlide + 1) % this.images.length;
    },
    prevSlide() {
      this.currentSlide = this.currentSlide === 0 ? this.images.length - 1 : this.currentSlide - 1;
    },
    openLightbox(index) {
      this.lightboxIndex = index;
      this.showLightbox = true;
    },
    closeLightbox() {
      this.showLightbox = false;
    },
    startAutoSlide() {
      if (this.images.length > 1) {
        this.autoSlideInterval = setInterval(() => {
          this.nextSlide();
        }, 5000);
      }
    },
    stopAutoSlide() {
      if (this.autoSlideInterval) {
        clearInterval(this.autoSlideInterval);
        this.autoSlideInterval = null;
      }
    }
  },
  mounted() {
    this.startAutoSlide();
  },
  beforeUnmount() {
    this.stopAutoSlide();
  }
}
</script>
