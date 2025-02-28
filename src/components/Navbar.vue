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
  </div></div>

</template>

<script>
export default {
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
    }
  },
  mounted() {
    document.getElementById("black").onclick = this.closenav;
    document.getElementById("hamburger").onclick = this.opennav;
  }

}
</script>
