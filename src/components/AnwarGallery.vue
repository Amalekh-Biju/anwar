<template>
    <div class="w-full overflow-hidden relative ">
        <div class="w-full lg:h-[600px] h-[250px]  block relative">
            <transition name="fade" mode="out-in">
                <img :key="currentImage" :src="images[currentImage]" 
                     class="lg:w-full lg:h-full w-[48rem] h-64 object-cover cursor-pointer" 
                     @click="openLightbox(currentImage)" />
            </transition>
            
            <!-- Image Status Dots -->
            <div class="absolute bottom-5 left-1/2 transform -translate-x-1/2 flex space-x-2">
                <div 
                    v-for="(_, index) in images" 
                    :key="index"
                    class="w-2 h-2 rounded-full bg-white cursor-pointer transition-opacity duration-300"
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
        <button class="absolute right-5 top-1/2 transform -translate-y-1/2 bg-white bg-opacity-50 p-2 mr-3 rounded-full"
            @click="nextImage">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                stroke="black" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                class="lucide lucide-chevron-right">
                <path d="M9 18l6-6-6-6" />
            </svg>
        </button>

    </div>

    <!-- Lightbox Component -->
    <Lightbox 
      :images="images"
      :is-visible="showLightbox"
      :initial-index="lightboxIndex"
      @close="closeLightbox"
    />
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
            currentImage: 0,
            showLightbox: false,
            lightboxIndex: 0
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
        openLightbox(index) {
            this.lightboxIndex = index;
            this.showLightbox = true;
        },
        closeLightbox() {
            this.showLightbox = false;
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
        }
    }
}
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.5s;
}

.fade-enter,
.fade-leave-to {
    opacity: 0;
}
</style>
