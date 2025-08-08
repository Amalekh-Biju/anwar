<template>
    <div class="w-full overflow-hidden relative ">
        

        <div class="w-full lg:h-[600px] h-[250px]  block relative">
            <transition name="fade" mode="out-in">
                <img :key="currentImage" :src="images[currentImage]" 
                     class="lg:w-full lg:h-full w-[48rem] h-64 object-cover cursor-pointer" 
                     @click="openFullscreen(currentImage)" />
            </transition>
            
            <!-- Image Status Dots -->
            <div class="absolute bottom-5 left-1/2 transform -translate-x-1/2 flex space-x-2">
                <div 
                    v-for="(_, index) in images" 
                    :key="index"
                    class="w-2 h-2 rounded-full  cursor-pointer transition-opacity duration-300"
                    :class="index === currentImage ? 'opacity-100' : 'opacity-20'"
                    @click="currentImage = index"
                ></div>
            </div>
        </div>

          <div class="w-screen justify-center">
            <div 
                class="absolute bottom-10 right-0 bg-white py-3 pr-8 lg:pr-10 mt-10 rounded-l-xl text-sm lg:text-xl flex items-center">
                <div class="gap-8 lg:gap-20 flex justify-center items-center ml-5">
                    <a href="tel:+919778238199" class="flex items-center gap-2">
                        <p>Call</p>
                        <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" class="lg:w-6 lg:h-6" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"></path></svg>
                    </a>
                    <a href="https://maps.app.goo.gl/9Tqf8iMFc9oprFQX6" class="flex items-center gap-2">
                        <p>Map</p>
                        <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" class="lg:w-6 lg:h-6" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 10c0 4.993-5.539 10.193-7.399 11.799a1 1 0 0 1-1.202 0C9.539 20.193 4 14.993 4 10a8 8 0 0 1 16 0"></path><circle cx="12" cy="10" r="3"></circle></svg>
                    </a>
                </div>
            </div>
        </div>

        <!-- Left Arrow -->
        <button class="absolute left-5 top-1/2 transform -translate-y-1/2 bg-white bg-opacity-50 p-2 ml-3 rounded-full"
            @click="prevImage">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                stroke="black" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                class="lucide lucide-chevron-left">
                <path d="M15 18l-6-6 6-6" />
            </svg>
        </button>

        <!-- Right Arrow -->
        <button class="absolute right-5 top-1/2  opatransform -translate-y-1/2 bg-white bg-opacity-50 p-2 mr-3 rounded-full"
            @click="nextImage">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                stroke="black" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                class="lucide lucide-chevron-right">
                <path d="M9 18l6-6-6-6" />
            </svg>
        </button>


    </div>

    <!-- Fullscreen overlay -->
    <div v-if="isFullscreen" class="fullscreen-modal" @click="closeFullscreen">
      <!-- Navigation header -->
      <div class="flex justify-between items-center p-4 bg-black bg-opacity-75" @click.stop>
        <span class="text-white">{{ currentImage + 1 }} / {{ images.length }}</span>
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
          :src="images[fullscreenIndex]" 
          :alt="`Gallery image ${fullscreenIndex + 1}`" 
          class="max-h-full max-w-full object-contain transition-all duration-300"
          :style="{ transform: `scale(${zoomLevel})` }"
        />
        
        <!-- Navigation buttons -->
        <button 
          @click="prevFullscreenImage" 
          class="nav-button nav-button-left"
          aria-label="Previous image"
          v-show="images.length > 1"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
          </svg>
        </button>
        
        <button 
          @click="nextFullscreenImage" 
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
</template>

<script>
export default {
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
            currentImage: 0,
            isFullscreen: false,
            fullscreenIndex: 0,
            zoomLevel: 1,
            minZoom: 0.5,
            maxZoom: 3
        };
    },
    mounted() {
        this.startCarousel();
    },
    methods: {
        prevImage() {
            this.currentImage = (this.currentImage - 1 + this.images.length) % this.images.length;
        },
        nextImage() {
            this.currentImage = (this.currentImage + 1) % this.images.length;
        },
        sharepage() {
            if (navigator.share) {
                navigator.share({
                    title: this.card.title,
                    text: this.card.description,
                    url: window.location.href
                })
                    .then(() => console.log('Successful share'))
                    .catch((error) => console.log('Error sharing', error));
            }
        },
        startCarousel() {
            setInterval(() => {
                this.currentImage = (this.currentImage + 1) % this.images.length;
            }, 6000);
        },
        openFullscreen(index) {
            this.fullscreenIndex = index;
            this.isFullscreen = true;
            this.zoomLevel = 1;
            document.body.classList.add('overflow-hidden');
        },
        closeFullscreen() {
            this.isFullscreen = false;
            this.zoomLevel = 1;
            document.body.classList.remove('overflow-hidden');
        },
        nextFullscreenImage() {
            this.fullscreenIndex = (this.fullscreenIndex + 1) % this.images.length;
            this.zoomLevel = 1;
        },
        prevFullscreenImage() {
            this.fullscreenIndex = (this.fullscreenIndex - 1 + this.images.length) % this.images.length;
            this.zoomLevel = 1;
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
            
            if (e.key === 'ArrowRight') this.nextFullscreenImage();
            if (e.key === 'ArrowLeft') this.prevFullscreenImage();
            if (e.key === 'Escape') this.closeFullscreen();
        }
    },
    mounted() {
        this.startCarousel();
        window.addEventListener('keydown', this.handleKeyDown);
    },
    beforeUnmount() {
        window.removeEventListener('keydown', this.handleKeyDown);
    }
};
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.55s ease;
    width: 100%;
    height: 100%;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}

a {
  text-decoration: none;
  color: inherit;
  position: relative;
}

nav a::after {
  content: "";
  position: absolute;
  width: 100%;
  transform: scaleX(0);
  height: 2px;
  bottom: 0;
  left: 0;
  background-color: #00b4d8;
  /* Change to your desired underline color */
  transform-origin: bottom right;
  transition: transform 0.3s ease;
}

nav a:hover::after {
  transform: scaleX(1);
  transform-origin: bottom left;
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
