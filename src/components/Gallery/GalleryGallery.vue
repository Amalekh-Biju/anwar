<template>
  <div class="gallery-container overflow-clip">
    <!-- Staggered gallery grid with fixed size images -->
    <div class="staggered-gallery">
      <div class="gallery-row">
        <div 
          v-for="(image, index) in topRowImages" 
          :key="`top-${index}`" 
          class="gallery-item"
        >
          <img 
            :src="image" 
            class="gallery-image cursor-pointer transition-transform hover:scale-105"
            @click="openFullscreen(index * 2)"
          />
        </div>
      </div>
      <div class="gallery-row gallery-row-offset">
        <div 
          v-for="(image, index) in bottomRowImages" 
          :key="`bottom-${index}`" 
          class="gallery-item"
        >
          <img 
            :src="image" 
            class="gallery-image cursor-pointer transition-transform hover:scale-105"
            @click="openFullscreen(index * 2 + 1)"
          />
        </div>
      </div>
    </div>
  


    <!-- Fullscreen overlay -->
    <div v-if="isFullscreen" class="fixed inset-0 bg-black z-50 flex flex-col">
      <!-- Navigation header -->
      <div class="flex justify-between items-center p-4 bg-black bg-opacity-75">
        <span class="text-white">{{ currentIndex + 1 }} / {{ images.length }}</span>
        <button 
          @click="closeFullscreen" 
          class="text-white p-2 rounded-full hover:bg-gray-800"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </div>

      <!-- Image container -->
      <div class="flex-grow flex items-center justify-center relative">
        <img 
          :src="images[currentIndex].src" 
          :alt="images[currentIndex].alt || ''" 
          class="max-h-full max-w-full object-contain"
        />
        
        <!-- Navigation buttons -->
        <button 
          @click="prevImage" 
          class="absolute left-4 p-2 rounded-full bg-black bg-opacity-50 text-white hover:bg-opacity-75"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
          </svg>
        </button>
        
        <button 
          @click="nextImage" 
          class="absolute right-4 p-2 rounded-full bg-black bg-opacity-50 text-white hover:bg-opacity-75"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
          </svg>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    images: {
      type: Array,
      required: true,
    }
  },
  data() {
    return {
      isFullscreen: false,
      currentIndex: 0
    }
  },
  computed: {
    topRowImages() {
      return this.images.filter((_, index) => index % 2 === 0);
    },
    bottomRowImages() {
      return this.images.filter((_, index) => index % 2 === 1);
    }
  },
  methods: {
    openFullscreen(index) {
      this.currentIndex = index;
      this.isFullscreen = true;
      document.body.classList.add('overflow-hidden');
    },
    closeFullscreen() {
      this.isFullscreen = false;
      document.body.classList.remove('overflow-hidden');
    },
    nextImage() {
      this.currentIndex = (this.currentIndex + 1) % this.images.length;
    },
    prevImage() {
      this.currentIndex = (this.currentIndex - 1 + this.images.length) % this.images.length;
    },
    handleKeyDown(e) {
      if (!this.isFullscreen) return;
      
      if (e.key === 'ArrowRight') this.nextImage();
      if (e.key === 'ArrowLeft') this.prevImage();
      if (e.key === 'Escape') this.closeFullscreen();
    }
  },
  mounted() {
    window.addEventListener('keydown', this.handleKeyDown);
  },
  beforeUnmount() {
    window.removeEventListener('keydown', this.handleKeyDown);
  }
}
</script>

<style scoped>
.staggered-gallery {
  width: 100%;
  overflow-x: hidden;
  position: relative;
}

.gallery-row {
  display: flex;
  width: max-content; /* Allows row to overflow */
  gap: 12px;
  margin-bottom: 12px;
}

.gallery-row-offset {
  margin-left: 100px; /* Creates staggered effect */
}

.gallery-item {
  width: 250px;
  height: 200px;
  overflow: hidden;
  border-radius: 8px;
}

.gallery-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 8px;
}
</style>