<template>
  <nav class="fixed top-0 left-0 right-0 bg-white/95 backdrop-blur-md border-b border-gray-200 z-50">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between items-center h-20">
        <!-- Logo -->
        <div class="flex-shrink-0">
          <a href="/" class="text-2xl lg:text-3xl font-bold text-gray-900 hover:text-blue-600 transition-colors">
            RUDRA GROUP
          </a>
        </div>

        <!-- Desktop Navigation -->
        <div class="hidden md:flex items-center space-x-8">
          <a 
            href="/" 
            class="text-gray-700 hover:text-blue-600 font-medium transition-colors duration-200"
            :class="{ 'text-blue-600 font-semibold': isCurrentPage('/') }"
          >
            Home
          </a>
          <a 
            href="/anwar-arena" 
            class="text-gray-700 hover:text-blue-600 font-medium transition-colors duration-200"
            :class="{ 'text-blue-600 font-semibold': isCurrentPage('/anwar-arena') }"
          >
            Anwar Arena
          </a>
          <a 
            href="/nirmala-mansion" 
            class="text-gray-700 hover:text-green-600 font-medium transition-colors duration-200"
            :class="{ 'text-green-600 font-semibold': isCurrentPage('/nirmala-mansion') }"
          >
            Nirmala Mansion
          </a>
          <a 
            href="#contact" 
            class="bg-blue-600 text-white px-6 py-2 rounded-full hover:bg-blue-700 transition-colors duration-200 font-medium"
          >
            Contact
          </a>
        </div>

        <!-- Mobile menu button -->
        <div class="md:hidden">
          <button 
            @click="toggleMobileMenu"
            class="text-gray-700 hover:text-blue-600 p-2 rounded-lg transition-colors"
            aria-label="Toggle mobile menu"
          >
            <svg 
              v-if="!mobileMenuOpen" 
              xmlns="http://www.w3.org/2000/svg" 
              width="24" 
              height="24" 
              viewBox="0 0 24 24" 
              fill="none" 
              stroke="currentColor" 
              stroke-width="2" 
              stroke-linecap="round" 
              stroke-linejoin="round"
            >
              <line x1="4" x2="20" y1="6" y2="6"/>
              <line x1="4" x2="20" y1="12" y2="12"/>
              <line x1="4" x2="20" y1="18" y2="18"/>
            </svg>
            <svg 
              v-else 
              xmlns="http://www.w3.org/2000/svg" 
              width="24" 
              height="24" 
              viewBox="0 0 24 24" 
              fill="none" 
              stroke="currentColor" 
              stroke-width="2" 
              stroke-linecap="round" 
              stroke-linejoin="round"
            >
              <path d="m18 6-12 12"/>
              <path d="m6 6 12 12"/>
            </svg>
          </button>
        </div>
      </div>
    </div>

    <!-- Mobile Menu -->
    <div 
      v-show="mobileMenuOpen" 
      class="md:hidden bg-white border-t border-gray-200 shadow-lg"
    >
      <div class="px-4 py-4 space-y-4">
        <a 
          href="/" 
          @click="closeMobileMenu"
          class="block text-gray-700 hover:text-blue-600 font-medium py-2 transition-colors"
          :class="{ 'text-blue-600 font-semibold': isCurrentPage('/') }"
        >
          Home
        </a>
        <a 
          href="/anwar-arena" 
          @click="closeMobileMenu"
          class="block text-gray-700 hover:text-blue-600 font-medium py-2 transition-colors"
          :class="{ 'text-blue-600 font-semibold': isCurrentPage('/anwar-arena') }"
        >
          Anwar Arena
        </a>
        <a 
          href="/nirmala-mansion" 
          @click="closeMobileMenu"
          class="block text-gray-700 hover:text-green-600 font-medium py-2 transition-colors"
          :class="{ 'text-green-600 font-semibold': isCurrentPage('/nirmala-mansion') }"
        >
          Nirmala Mansion
        </a>
        <a 
          href="#contact" 
          @click="closeMobileMenu"
          class="block bg-blue-600 text-white text-center px-6 py-3 rounded-full hover:bg-blue-700 transition-colors font-medium"
        >
          Contact
        </a>
      </div>
    </div>

    <!-- Scroll to Top Button -->
    <button 
      v-show="showScrollButton"
      @click="scrollToTop" 
      class="fixed bottom-6 left-6 bg-gray-800 hover:bg-gray-900 text-white p-3 rounded-full shadow-lg z-40 transition-all duration-300 hover:scale-110"
      aria-label="Scroll to top"
    >
      <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <path d="m18 15-6-6-6 6"/>
      </svg>
    </button>
  </nav>
</template>

<script>
export default {
  name: 'Navbar',
  data() {
    return {
      mobileMenuOpen: false,
      showScrollButton: false
    }
  },
  methods: {
    toggleMobileMenu() {
      this.mobileMenuOpen = !this.mobileMenuOpen;
      // Prevent body scroll when mobile menu is open
      if (this.mobileMenuOpen) {
        document.body.style.overflow = 'hidden';
      } else {
        document.body.style.overflow = 'auto';
      }
    },
    closeMobileMenu() {
      this.mobileMenuOpen = false;
      document.body.style.overflow = 'auto';
    },
    scrollToTop() {
      window.scrollTo({
        top: 0,
        behavior: 'smooth'
      });
    },
    handleScroll() {
      this.showScrollButton = window.scrollY > 300;
    },
    isCurrentPage(path) {
      if (typeof window !== 'undefined') {
        const currentPath = window.location.pathname;
        if (path === '/') {
          return currentPath === '/' || currentPath === '';
        }
        return currentPath.includes(path);
      }
      return false;
    }
  },
  mounted() {
    // Add scroll event listener
    window.addEventListener('scroll', this.handleScroll);
    
    // Close mobile menu when clicking outside
    document.addEventListener('click', (e) => {
      if (this.mobileMenuOpen && !e.target.closest('nav')) {
        this.closeMobileMenu();
      }
    });
  },
  beforeUnmount() {
    // Clean up event listeners
    window.removeEventListener('scroll', this.handleScroll);
    document.body.style.overflow = 'auto';
  }
}
</script>

<style scoped>
/* Additional styles if needed */
nav {
  transition: all 0.3s ease;
}

/* Smooth transitions for mobile menu */
.md\:hidden > div {
  transition: all 0.3s ease;
}
</style>
