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
            :alt="`Gallery image ${getOriginalIndex(index, true) + 1}`"
            @click="openFullscreen(getOriginalIndex(index, true))"
            loading="lazy"
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
            :alt="`Gallery image ${getOriginalIndex(index, false) + 1}`"
            @click="openFullscreen(getOriginalIndex(index, false))"
            loading="lazy"
          />
        </div>
      </div>
    </div>

    <!-- Fullscreen overlay -->
    <div v-if="isFullscreen" class="fullscreen-modal" @click="closeFullscreen">
      <!-- Navigation header -->
      <div class="flex justify-between items-center p-4 bg-black bg-opacity-75" @click.stop>
        <span class="text-white">{{ currentIndex + 1 }} / {{ images.length }}</span>
        <button 
          @click="closeFullscreen" 
          class="text-white p-2 rounded-full hover:bg-gray-800"
          aria-label="Close fullscreen"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </div>

      <!-- Image container -->
      <div class="flex-grow flex items-center justify-center relative" @click.stop>
        <img 
          :src="images[currentIndex]" 
          :alt="`Gallery image ${currentIndex + 1}`" 
          class="max-h-full max-w-full object-contain transition-all duration-300"
          :style="{ transform: `scale(${zoomLevel})` }"
          @load="onImageLoad"
          @error="onImageError"
        />
        
        <!-- Navigation buttons -->
        <button 
          @click="prevImage" 
          class="nav-button nav-button-left"
          aria-label="Previous image"
          v-show="images.length > 1"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
          </svg>
        </button>
        
        <button 
          @click="nextImage" 
          class="nav-button nav-button-right"
          aria-label="Next image"
          v-show="images.length > 1"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
          </svg>
        </button>

        <!-- Zoom controls -->
        <div class="absolute bottom-4 left-1/2 transform -translate-x-1/2 flex gap-4">
          <button 
            @click="zoomOut" 
            class="bg-black bg-opacity-75 text-white p-2 rounded-full hover:bg-opacity-90"
            aria-label="Zoom out"
          >
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0zM13 10H9" />
            </svg>
          </button>
          <button 
            @click="zoomIn" 
            class="bg-black bg-opacity-75 text-white p-2 rounded-full hover:bg-opacity-90"
            aria-label="Zoom in"
          >
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0zM10 7v3m0 0v3m0-3h3m-3 0H7" />
            </svg>
          </button>
        </div>
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
      currentIndex: 0,
      zoomLevel: 1,
      minZoom: 0.5,
      maxZoom: 3
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
    getOriginalIndex(rowIndex, isTopRow) {
      // Map split row indices back to original array indices
      return isTopRow ? rowIndex * 2 : rowIndex * 2 + 1;
    },
    openFullscreen(index) {
      // Ensure index is within bounds
      if (index >= 0 && index < this.images.length) {
        this.currentIndex = index;
        this.isFullscreen = true;
        document.body.classList.add('overflow-hidden');
      }
    },
    closeFullscreen() {
      this.isFullscreen = false;
      this.zoomLevel = 1; // Reset zoom when closing
      document.body.classList.remove('overflow-hidden');
    },
    nextImage() {
      this.currentIndex = (this.currentIndex + 1) % this.images.length;
      this.zoomLevel = 1; // Reset zoom when changing images
    },
    prevImage() {
      this.currentIndex = (this.currentIndex - 1 + this.images.length) % this.images.length;
      this.zoomLevel = 1; // Reset zoom when changing images
    },
    zoomIn() {
      if (this.zoomLevel < this.maxZoom) {
        this.zoomLevel = Math.min(this.zoomLevel + 0.25, this.maxZoom);
      }
    },
    zoomOut() {
      if (this.zoomLevel > this.minZoom) {
        this.zoomLevel = Math.max(this.zoomLevel - 0.25, this.minZoom);
      }
    },
    handleKeyDown(e) {
      if (!this.isFullscreen) return;
      
      if (e.key === 'ArrowRight') this.nextImage();
      if (e.key === 'ArrowLeft') this.prevImage();
      if (e.key === 'Escape') this.closeFullscreen();
    },
    onImageLoad() {
      // Image loaded successfully
      console.log('Image loaded');
    },
    onImageError() {
      // Handle image loading error
      console.error('Failed to load image');
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

@media (max-width: 768px) {
  .gallery-row-offset {
    margin-left: 50px; /* Smaller offset on mobile */
  }
  
  .gallery-item {
    width: 200px;
    height: 150px;
  }
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

/* Fullscreen Modal Styles */
.fullscreen-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.95);
  z-index: 9999;
  display: flex;
  flex-direction: column;
  backdrop-filter: blur(2px);
}

.fullscreen-modal img {
  user-select: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
}

/* Navigation buttons */
.nav-button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  padding: 12px;
  border-radius: 50%;
  background-color: rgba(0, 0, 0, 0.6);
  color: white;
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
  z-index: 10000;
}

.nav-button:hover {
  background-color: rgba(0, 0, 0, 0.8);
  transform: translateY(-50%) scale(1.1);
}

.nav-button-left {
  left: 20px;
}

.nav-button-right {
  right: 20px;
}

/* Close button styling */
.fullscreen-modal button[aria-label="Close fullscreen"] {
  transition: all 0.3s ease;
}

.fullscreen-modal button[aria-label="Close fullscreen"]:hover {
  background-color: rgba(255, 255, 255, 0.2);
  transform: scale(1.1);
}

/* Mobile responsive styles for fullscreen modal */
@media (max-width: 768px) {
  .nav-button-left {
    left: 10px;
  }
  
  .nav-button-right {
    right: 10px;
  }
  
  .nav-button {
    padding: 8px;
  }
  
  .fullscreen-modal .flex.justify-between {
    padding: 12px;
  }
}
</style>