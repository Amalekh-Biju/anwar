<template>
  <div 
    v-if="isVisible" 
    class="fixed inset-0 z-[9999] bg-black bg-opacity-90 flex items-center justify-center p-4"
    @click="handleOverlayClick"
    @keydown.esc="closeLightbox"
    tabindex="0"
  >
    <!-- Close button -->
    <button 
      @click="closeLightbox"
      class="absolute top-4 right-4 z-[10000] text-white hover:text-gray-300 p-2 rounded-full bg-black bg-opacity-50 hover:bg-opacity-70 transition-all"
    >
      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <path d="m18 6-12 12"/>
        <path d="m6 6 12 12"/>
      </svg>
    </button>

    <!-- Previous button -->
    <button 
      v-if="images.length > 1"
      @click="previousImage"
      class="absolute left-4 top-1/2 transform -translate-y-1/2 z-[10000] text-white hover:text-gray-300 p-3 rounded-full bg-black bg-opacity-50 hover:bg-opacity-70 transition-all"
    >
      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <path d="m15 18-6-6 6-6"/>
      </svg>
    </button>

    <!-- Next button -->
    <button 
      v-if="images.length > 1"
      @click="nextImage"
      class="absolute right-4 top-1/2 transform -translate-y-1/2 z-[10000] text-white hover:text-gray-300 p-3 rounded-full bg-black bg-opacity-50 hover:bg-opacity-70 transition-all"
    >
      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <path d="m9 18 6-6-6 6"/>
      </svg>
    </button>

    <!-- Image container with zoom -->
    <div 
      class="relative max-w-full max-h-full overflow-hidden"
      @wheel="handleWheel"
    >
      <img 
        ref="lightboxImage"
        :src="currentImage"
        :alt="`Image ${currentIndex + 1}`"
        class="max-w-full max-h-full object-contain cursor-zoom-in transition-transform duration-200"
        :style="{ transform: `scale(${zoomLevel}) translate(${translateX}px, ${translateY}px)` }"
        @click="toggleZoom"
        @mousedown="startDrag"
        @mousemove="onDrag"
        @mouseup="endDrag"
        @mouseleave="endDrag"
        :class="{ 'cursor-zoom-out': zoomLevel > 1, 'cursor-grab': isDragging }"
      />
    </div>

    <!-- Image counter -->
    <div class="absolute bottom-4 left-1/2 transform -translate-x-1/2 text-white bg-black bg-opacity-50 px-4 py-2 rounded-full">
      {{ currentIndex + 1 }} / {{ images.length }}
    </div>

    <!-- Zoom controls -->
    <div class="absolute bottom-4 right-4 flex gap-2">
      <button 
        @click="zoomOut"
        class="text-white hover:text-gray-300 p-2 rounded-full bg-black bg-opacity-50 hover:bg-opacity-70 transition-all"
        :disabled="zoomLevel <= 1"
      >
        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <circle cx="11" cy="11" r="8"/>
          <path d="M21 21l-4.35-4.35"/>
          <path d="M8 11h6"/>
        </svg>
      </button>
      <button 
        @click="zoomIn"
        class="text-white hover:text-gray-300 p-2 rounded-full bg-black bg-opacity-50 hover:bg-opacity-70 transition-all"
        :disabled="zoomLevel >= 4"
      >
        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <circle cx="11" cy="11" r="8"/>
          <path d="M21 21l-4.35-4.35"/>
          <path d="M11 8v6"/>
          <path d="M8 11h6"/>
        </svg>
      </button>
      <button 
        @click="resetZoom"
        class="text-white hover:text-gray-300 p-2 rounded-full bg-black bg-opacity-50 hover:bg-opacity-70 transition-all"
      >
        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M3 12a9 9 0 1 0 9-9 9.75 9.75 0 0 0-6.74 2.74L3 8"/>
          <path d="M3 3v5h5"/>
        </svg>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    images: {
      type: Array,
      required: true
    },
    isVisible: {
      type: Boolean,
      default: false
    },
    initialIndex: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      currentIndex: 0,
      zoomLevel: 1,
      translateX: 0,
      translateY: 0,
      isDragging: false,
      dragStart: { x: 0, y: 0 },
      lastTranslate: { x: 0, y: 0 }
    }
  },
  computed: {
    currentImage() {
      return this.images[this.currentIndex] || '';
    }
  },
  watch: {
    isVisible(newVal) {
      if (newVal) {
        this.currentIndex = this.initialIndex;
        this.resetZoom();
        document.body.style.overflow = 'hidden';
        this.$nextTick(() => {
          this.$el?.focus();
        });
      } else {
        document.body.style.overflow = 'auto';
      }
    },
    currentIndex() {
      this.resetZoom();
    }
  },
  methods: {
    closeLightbox() {
      this.$emit('close');
    },
    handleOverlayClick(event) {
      if (event.target === event.currentTarget) {
        this.closeLightbox();
      }
    },
    nextImage() {
      this.currentIndex = (this.currentIndex + 1) % this.images.length;
    },
    previousImage() {
      this.currentIndex = this.currentIndex === 0 ? this.images.length - 1 : this.currentIndex - 1;
    },
    zoomIn() {
      if (this.zoomLevel < 4) {
        this.zoomLevel = Math.min(this.zoomLevel + 0.5, 4);
      }
    },
    zoomOut() {
      if (this.zoomLevel > 1) {
        this.zoomLevel = Math.max(this.zoomLevel - 0.5, 1);
        if (this.zoomLevel === 1) {
          this.translateX = 0;
          this.translateY = 0;
        }
      }
    },
    resetZoom() {
      this.zoomLevel = 1;
      this.translateX = 0;
      this.translateY = 0;
    },
    toggleZoom(event) {
      if (this.zoomLevel === 1) {
        this.zoomLevel = 2;
      } else {
        this.resetZoom();
      }
    },
    handleWheel(event) {
      event.preventDefault();
      const delta = event.deltaY > 0 ? -0.2 : 0.2;
      const newZoom = Math.max(1, Math.min(4, this.zoomLevel + delta));
      
      if (newZoom !== this.zoomLevel) {
        this.zoomLevel = newZoom;
        if (this.zoomLevel === 1) {
          this.translateX = 0;
          this.translateY = 0;
        }
      }
    },
    startDrag(event) {
      if (this.zoomLevel > 1) {
        this.isDragging = true;
        this.dragStart = { x: event.clientX, y: event.clientY };
        this.lastTranslate = { x: this.translateX, y: this.translateY };
        event.preventDefault();
      }
    },
    onDrag(event) {
      if (this.isDragging && this.zoomLevel > 1) {
        const deltaX = event.clientX - this.dragStart.x;
        const deltaY = event.clientY - this.dragStart.y;
        
        this.translateX = this.lastTranslate.x + deltaX / this.zoomLevel;
        this.translateY = this.lastTranslate.y + deltaY / this.zoomLevel;
      }
    },
    endDrag() {
      this.isDragging = false;
    },
    handleKeydown(event) {
      if (!this.isVisible) return;
      
      switch(event.key) {
        case 'Escape':
          this.closeLightbox();
          break;
        case 'ArrowLeft':
          this.previousImage();
          break;
        case 'ArrowRight':
          this.nextImage();
          break;
        case '+':
        case '=':
          this.zoomIn();
          break;
        case '-':
          this.zoomOut();
          break;
        case '0':
          this.resetZoom();
          break;
      }
    }
  },
  mounted() {
    // Add keyboard event listeners
    document.addEventListener('keydown', this.handleKeydown);
  },
  beforeUnmount() {
    document.removeEventListener('keydown', this.handleKeydown);
    document.body.style.overflow = 'auto';
  }
}
</script>

<style scoped>
.cursor-zoom-in {
  cursor: zoom-in;
}
.cursor-zoom-out {
  cursor: zoom-out;
}
.cursor-grab {
  cursor: grab;
}
.cursor-grabbing {
  cursor: grabbing;
}
</style>