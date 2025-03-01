<template>

<div>
  
  <div id="bar">
      <div id="black" class="absolute w-full bg-black h-full right-0 top-0 z-10 opacity-50 hidden" />
      <div id="nav" class="absolute left-0 top-0 h-full w-4/5 bg-white z-10 p-0 hidden">

        <div class="w-full h-20 flex flex-col justify-center pl-10">

          <a href="/" class="">
            <h1 class="font-bold text-xl lg:text-3xl text-left">NELLUPURA BY TEJUS</h1>
          </a>


        </div>
        <div class="w-full h-[2px] bg-gray-300" />

        <nav class="flex flex-col p-10 gap-10 [&>*>*]:flex [&>*>*]:gap-5 [&>*>*]:justify-between [&>*>*]:font-semibold">
            <button @click="closenav"><a href="#exp"> Experiences <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24"
              viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
              stroke-linejoin="round" class="lucide lucide-arrow-right">
              <path d="M5 12h14" />
              <path d="m12 5 7 7-7 7" />
              </svg> </a> </button>
            <button @click="closenav"><a href="#gallery"> Gallery <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24"
              viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
              stroke-linejoin="round" class="lucide lucide-arrow-right">
              <path d="M5 12h14" />
              <path d="m12 5 7 7-7 7" />
              </svg> </a> </button>
            <button @click="closenav"><a href="#stay"> Stays <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24"
              viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
              stroke-linejoin="round" class="lucide lucide-arrow-right">
              <path d="M5 12h14" />
              <path d="m12 5 7 7-7 7" />
              </svg> </a> </button>
            <button @click="closenav"><a href="#about"> About Us <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24"
              viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
              stroke-linejoin="round" class="lucide lucide-arrow-right">
              <path d="M5 12h14" />
              <path d="m12 5 7 7-7 7" />
              </svg> </a> </button>
            <button><a href="#contact"> Contact <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24"
              viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
              stroke-linejoin="round" class="lucide lucide-arrow-right">
              <path d="M5 12h14" />
              <path d="m12 5 7 7-7 7" />
              </svg> </a> </button>
        </nav>
      </div>
    </div>

  <div class="flex items-center justify-between px-8 py-12 w-screen bg-white ">

    <a href="/">
      <h1 class="font-bold text-xl lg:text-3xl text-right">NELLUPURA BY TEJUS</h1>
    </a>

    <button id="hamburger" class="p-2 rounded-full lg:hidden">
      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
        stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
        class="lucide lucide-menu">
        <line x1="4" x2="20" y1="12" y2="12" />
        <line x1="4" x2="20" y1="6" y2="6" />
        <line x1="4" x2="20" y1="18" y2="18" />
      </svg>
    </button>



    <div class="[&>a]:font-medium [&>a]:text-2xl lg:flex hidden gap-10 ">
      <a href="#exp">Experiences</a>
      <a href="#gallery">Gallery</a>
      <a href="#stay">Stays</a>
      <a href="#about">About Us</a>
      <a href="#contact">Contact</a>
    </div>
  </div>
  
  <!-- Scroll to top button -->
  <a class="fixed bottom-8 right-8 rounded-full bg-white border-gray-200 border-2 p-4 shadow-lg z-20 transition-opacity duration-300" :class="{ 'opacity-100': !showScrollButton, 'opacity-0': showScrollButton }" href="https://wa.me/+919778238199"><svg viewBox="0 0 256 259" width="36" height="39" xmlns="http://www.w3.org/2000/svg" preserveAspectRatio="xMidYMid"><path d="m67.663 221.823 4.185 2.093c17.44 10.463 36.971 15.346 56.503 15.346 61.385 0 111.609-50.224 111.609-111.609 0-29.297-11.859-57.897-32.785-78.824-20.927-20.927-48.83-32.785-78.824-32.785-61.385 0-111.61 50.224-110.912 112.307 0 20.926 6.278 41.156 16.741 58.594l2.79 4.186-11.16 41.156 41.853-10.464Z" fill="#00E676"/><path d="M219.033 37.668C195.316 13.254 162.531 0 129.048 0 57.898 0 .698 57.897 1.395 128.35c0 22.322 6.278 43.947 16.742 63.478L0 258.096l67.663-17.439c18.834 10.464 39.76 15.347 60.688 15.347 70.453 0 127.653-57.898 127.653-128.35 0-34.181-13.254-66.269-36.97-89.986ZM129.048 234.38c-18.834 0-37.668-4.882-53.712-14.648l-4.185-2.093-40.458 10.463 10.463-39.76-2.79-4.186C7.673 134.63 22.322 69.058 72.546 38.365c50.224-30.692 115.097-16.043 145.79 34.181 30.692 50.224 16.043 115.097-34.18 145.79-16.045 10.463-35.576 16.043-55.108 16.043Zm61.385-77.428-7.673-3.488s-11.16-4.883-18.136-8.371c-.698 0-1.395-.698-2.093-.698-2.093 0-3.488.698-4.883 1.396 0 0-.697.697-10.463 11.858-.698 1.395-2.093 2.093-3.488 2.093h-.698c-.697 0-2.092-.698-2.79-1.395l-3.488-1.395c-7.673-3.488-14.648-7.674-20.229-13.254-1.395-1.395-3.488-2.79-4.883-4.185-4.883-4.883-9.766-10.464-13.253-16.742l-.698-1.395c-.697-.698-.697-1.395-1.395-2.79 0-1.395 0-2.79.698-3.488 0 0 2.79-3.488 4.882-5.58 1.396-1.396 2.093-3.488 3.488-4.883 1.395-2.093 2.093-4.883 1.395-6.976-.697-3.488-9.068-22.322-11.16-26.507-1.396-2.093-2.79-2.79-4.883-3.488H83.01c-1.396 0-2.79.698-4.186.698l-.698.697c-1.395.698-2.79 2.093-4.185 2.79-1.395 1.396-2.093 2.79-3.488 4.186-4.883 6.278-7.673 13.951-7.673 21.624 0 5.58 1.395 11.161 3.488 16.044l.698 2.093c6.278 13.253 14.648 25.112 25.81 35.575l2.79 2.79c2.092 2.093 4.185 3.488 5.58 5.58 14.649 12.557 31.39 21.625 50.224 26.508 2.093.697 4.883.697 6.976 1.395h6.975c3.488 0 7.673-1.395 10.464-2.79 2.092-1.395 3.487-1.395 4.882-2.79l1.396-1.396c1.395-1.395 2.79-2.092 4.185-3.487 1.395-1.395 2.79-2.79 3.488-4.186 1.395-2.79 2.092-6.278 2.79-9.765v-4.883s-.698-.698-2.093-1.395Z" fill="#FFF"/></svg><div class="h-3 w-3 bg-red-500 absolute rounded-full top-5 right-3 z-20"/> <div class="h-3 w-3 bg-red-500 absolute rounded-full top-5 right-3 animate-ping"/></a>

  <button 
    @click="scrollToTop" 
    class="fixed bottom-8 right-8 bg-white p-3 rounded-full shadow-lg z-20 transition-opacity duration-300 flex items-center gap-2"
    :class="{ 'opacity-0': !showScrollButton, 'opacity-100': showScrollButton }"
    aria-label="Scroll to top">
    Scroll To Top
    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
      stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
      class="lucide lucide-chevron-up">
      <path d="m18 15-6-6-6 6"/>
    </svg>
  </button>
</div>

</template>

<script>
export default {
  data() {
    return {
      showScrollButton: false,
    }
  },
  methods: {
    closenav() {
      document.getElementById("nav").classList.add("hidden");
      document.getElementById("black").classList.add("hidden");
      document.body.style.overflow = 'auto';
    },
    opennav() {
      const navElement = document.getElementById("nav");
      document.getElementById("black").classList.remove("hidden");
      document.body.style.overflow = 'hidden';
      navElement.classList.add("open");
      navElement.classList.remove("hidden");
    },
    scrollToTop() {
      window.scrollTo({
        top: 0,
        behavior: 'smooth'
      });
    },
    handleScroll() {
      // Show button when page is scrolled down enough (e.g., 300px)
      this.showScrollButton = window.scrollY > 300;
    }
  },
  mounted() {
    document.getElementById("black").onclick = this.closenav;
    document.getElementById("hamburger").onclick = this.opennav;
    
    // Add scroll event listener
    window.addEventListener('scroll', this.handleScroll);
  },
  beforeUnmount() {
    // Remove event listener when component is unmounted
    window.removeEventListener('scroll', this.handleScroll);
  }
}
</script>
