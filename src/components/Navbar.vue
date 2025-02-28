<template>

  <div class="flex items-center justify-between px-8 py-12 w-screen bg-white ">
    
    <a href="/">
      <h1 class="font-bold text-xl lg:text-3xl text-right">NELLUPURA BY TEJUS</h1>
    </a>
    
    <button id="hamburger" class="p-2 rounded-full">
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
      <a href="">Gallery</a>
      <a href="#stay">Stays</a>
      <a href="#about">About Us</a>
      <a href="#contact">Contact</a>
    </div>
  </div>
  
  </template>