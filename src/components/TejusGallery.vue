<template>
    <div class="w-full overflow-hidden relative">


        <div class="w-full lg:h-[600px] h-[250px]  block relative">
            <transition name="fade" mode="out-in">
                <img :key="currentImage" :src="images[currentImage]" class="lg:w-full lg:h-full w-[48rem] h-64 object-cover" />
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

        <div class="w-screen justify-center hidden lg:flex">
            <div 
                class="absolute bottom-10 right-0 bg-white py-3 pr-10 mt-10 rounded-l-xl lg:text-xl text-sm flex items-center">
                <div class=" gap-20 flex justify-center items-center ml-5">
                    <a href="" class="flex items-center gap-2 bg-[#25D366] p-2 rounded-full">
                        <svg viewBox="0 0 256 259" width="32" height="32" xmlns="http://www.w3.org/2000/svg" preserveAspectRatio="xMidYMid"><path d="m67.663 221.823 4.185 2.093c17.44 10.463 36.971 15.346 56.503 15.346 61.385 0 111.609-50.224 111.609-111.609 0-29.297-11.859-57.897-32.785-78.824-20.927-20.927-48.83-32.785-78.824-32.785-61.385 0-111.61 50.224-110.912 112.307 0 20.926 6.278 41.156 16.741 58.594l2.79 4.186-11.16 41.156 41.853-10.464Z" fill="#00E676"/><path d="M219.033 37.668C195.316 13.254 162.531 0 129.048 0 57.898 0 .698 57.897 1.395 128.35c0 22.322 6.278 43.947 16.742 63.478L0 258.096l67.663-17.439c18.834 10.464 39.76 15.347 60.688 15.347 70.453 0 127.653-57.898 127.653-128.35 0-34.181-13.254-66.269-36.97-89.986ZM129.048 234.38c-18.834 0-37.668-4.882-53.712-14.648l-4.185-2.093-40.458 10.463 10.463-39.76-2.79-4.186C7.673 134.63 22.322 69.058 72.546 38.365c50.224-30.692 115.097-16.043 145.79 34.181 30.692 50.224 16.043 115.097-34.18 145.79-16.045 10.463-35.576 16.043-55.108 16.043Zm61.385-77.428-7.673-3.488s-11.16-4.883-18.136-8.371c-.698 0-1.395-.698-2.093-.698-2.093 0-3.488.698-4.883 1.396 0 0-.697.697-10.463 11.858-.698 1.395-2.093 2.093-3.488 2.093h-.698c-.697 0-2.092-.698-2.79-1.395l-3.488-1.395c-7.673-3.488-14.648-7.674-20.229-13.254-1.395-1.395-3.488-2.79-4.883-4.185-4.883-4.883-9.766-10.464-13.253-16.742l-.698-1.395c-.697-.698-.697-1.395-1.395-2.79 0-1.395 0-2.79.698-3.488 0 0 2.79-3.488 4.882-5.58 1.396-1.396 2.093-3.488 3.488-4.883 1.395-2.093 2.093-4.883 1.395-6.976-.697-3.488-9.068-22.322-11.16-26.507-1.396-2.093-2.79-2.79-4.883-3.488H83.01c-1.396 0-2.79.698-4.186.698l-.698.697c-1.395.698-2.79 2.093-4.185 2.79-1.395 1.396-2.093 2.79-3.488 4.186-4.883 6.278-7.673 13.951-7.673 21.624 0 5.58 1.395 11.161 3.488 16.044l.698 2.093c6.278 13.253 14.648 25.112 25.81 35.575l2.79 2.79c2.092 2.093 4.185 3.488 5.58 5.58 14.649 12.557 31.39 21.625 50.224 26.508 2.093.697 4.883.697 6.976 1.395h6.975c3.488 0 7.673-1.395 10.464-2.79 2.092-1.395 3.487-1.395 4.882-2.79l1.396-1.396c1.395-1.395 2.79-2.092 4.185-3.487 1.395-1.395 2.79-2.79 3.488-4.186 1.395-2.79 2.092-6.278 2.79-9.765v-4.883s-.698-.698-2.093-1.395Z" fill="#FFF"/></svg>
                    </a>
                    <a href="" class="flex items-center gap-2">
                        <p>Call</p>
                        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-phone"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"></path></svg>
                    </a>
                    <a href="" class="flex items-center gap-2">
                        <p>Map </p>
                        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-map-pin"><path d="M20 10c0 4.993-5.539 10.193-7.399 11.799a1 1 0 0 1-1.202 0C9.539 20.193 4 14.993 4 10a8 8 0 0 1 16 0"></path><circle cx="12" cy="10" r="3"></circle></svg>
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
        }
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


</style>
