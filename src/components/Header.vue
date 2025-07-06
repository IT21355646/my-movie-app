<template>
  <header class="main-header">
    <div class="logo">
      <img src="../assets/Logos/Logo White.svg" alt="Movie App Logo" />
    </div>
    <div class="nav-container">
      <nav class="main-nav">
        <ul>
          <li><a href="#">HOME</a></li>
          <li><a href="#">OUR SCREENS</a></li>
          <li><a href="#">SCHEDULE</a></li>
          <li><a href="#">MOVIE LIBRARY</a></li>
          <li class="tablet-hide"><a href="#">LOCATION & CONTACT</a></li>
        </ul>
      </nav>
      <button class="hamburger-menu-icon" :class="{ 'active': isMobileMenuOpen }" @click="toggleMobileMenu">
        <img :src="menuIconSrc" alt="Menu" @error="handleImageError" />
      </button>
    </div>
    <div class="hamburger-backdrop" :class="{ 'active': isMobileMenuOpen }" @click="toggleMobileMenu"></div>
    <nav class="hamburger-nav" :class="{ 'mobile-open': isMobileMenuOpen }">
      <ul>
        <!-- Desktop view -->
        <li class="desktop-only"><a href="#">GALLERY</a></li>
        <!-- Tablet view -->
        <li class="tablet-only"><a href="#">LOCATION & CONTACT</a></li>
        <li class="tablet-only"><a href="#">GALLERY</a></li>
        <!-- Mobile view -->
        <li class="mobile-only"><a href="#">HOME</a></li>
        <li class="mobile-only"><a href="#">OUR SCREENS</a></li>
        <li class="mobile-only"><a href="#">SCHEDULE</a></li>
        <li class="mobile-only"><a href="#">MOVIE LIBRARY</a></li>
        <li class="mobile-only"><a href="#">LOCATION & CONTACT</a></li>
        <li class="mobile-only"><a href="#">GALLERY</a></li>
      </ul>
    </nav>
  </header>
</template>

<script>
export default {
  name: 'AppHeader',
  data() {
    return {
      isMobileMenuOpen: false,
    };
  },
  computed: {
    menuIconSrc() {
      return this.isMobileMenuOpen 
        ? new URL('../assets/Icons/Close White.svg', import.meta.url).href
        : new URL('../assets/Icons/Menu White.svg', import.meta.url).href;
    }
  },
  mounted() {
    // Event listener to close mobile menu on resize to desktop size
    window.addEventListener('resize', this.handleResize);
  },
  beforeUnmount() {
    // Remove event listener when component is unmounted
    window.removeEventListener('resize', this.handleResize);
  },
  methods: {
    toggleMobileMenu() {
      this.isMobileMenuOpen = !this.isMobileMenuOpen;
      // Prevent body scrolling when mobile menu is open
      document.body.style.overflow = this.isMobileMenuOpen ? 'hidden' : '';
    },
    handleResize() {
      // Close mobile menu if window is resized to desktop width
      if (window.innerWidth > 768 && this.isMobileMenuOpen) {
        this.isMobileMenuOpen = false;
        document.body.style.overflow = ''; // Re-enable scrolling
      }
    },
    handleImageError(event) {
      console.error('Image failed to load:', event.target.src);
    }
  }
};
</script>

<style lang="css" scoped>
.main-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 8px 0;
  background-color: #000;
  color: #fff;
  min-height: 56px;
  position: sticky;
  top: 0;
  z-index: 1000;
  border-bottom: 1px solid #252424;
  width: 100vw;
  margin-left: calc(-50vw + 50%);
  margin-right: calc(-50vw + 50%);
  overflow-x: hidden;
  box-sizing: border-box;
}

.logo img {
  height: 36px;
  margin-left: 20px;
  transition: height 0.3s ease;
}

/* Navigation Container */
.nav-container {
  display: flex;
  align-items: center;
  margin-right: 20px;
}

/* Desktop Navigation */
.main-nav {
  margin-right: 15px;
}

.main-nav ul {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
}

.main-nav li {
  margin-left: 20px;
}

.main-nav a {
  color: #fff;
  text-decoration: none;
  font-weight: normal;
  font-size: 13px;
  padding: 8px 0;
  display: block;
  transition: text-decoration 0.3s ease;
  border-bottom: 2px solid transparent;
}

.main-nav a:hover {
  text-decoration: underline;
  text-underline-offset: 4px;
}

/* Hamburger Menu Icon */
.hamburger-menu-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 44px;
  height: 44px;
  background: transparent;
  border: none;
  outline: none;
  cursor: pointer;
  padding: 10px;
  z-index: 1001;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

.hamburger-menu-icon:hover {
  background-color: rgba(255, 255, 255, 0.1);
}

.hamburger-menu-icon img {
  width: 20px;
  height: 20px;
  transition: all 0.3s ease-in-out;
}

.hamburger-menu-icon.active img {
  opacity: 0.9;
  transform: scale(1.1);
}

/* Hamburger Backdrop */
.hamburger-backdrop {
  display: none;
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(2px);
  z-index: 998;
  opacity: 0;
  transition: opacity 0.3s ease-in-out;
}

.hamburger-backdrop.active {
  display: block;
  opacity: 1;
}

/* Hamburger Navigation */
.hamburger-nav {
  display: none;
  position: fixed;
  top: 56px;
  right: 0;
  width: 320px;
  max-width: calc(100vw - 20px);
  height: calc(100vh - 56px);
  background-color: #000;
  border-left: 1px solid #252424;
  z-index: 999;
  opacity: 0;
  transform: translateX(100%);
  transition: all 0.3s ease-in-out;
  overflow-y: auto;
  box-shadow: -2px 0 10px rgba(0, 0, 0, 0.3);
}

.hamburger-nav.mobile-open {
  display: block;
  opacity: 1;
  transform: translateX(0);
}

.hamburger-nav ul {
  list-style: none;
  margin: 0;
  padding: 40px 0 20px 0;
  flex-direction: column;
  text-align: left;
}

.hamburger-nav li {
  margin: 0;
}

.hamburger-nav a {
  color: #fff;
  text-decoration: none;
  font-weight: normal;
  font-size: 14px;
  padding: 16px 20px;
  display: block;
  transition: background-color 0.3s ease;
  margin: 0 20px 0 20px;
  border-radius: 6px;
  min-height: 44px;
  display: flex;
  align-items: center;
}

.hamburger-nav a:hover {
  background-color: #252424;
  text-decoration: none;
}

/* Desktop hamburger */
.hamburger-nav .desktop-only {
  display: block;
}

.hamburger-nav .tablet-only,
.hamburger-nav .mobile-only {
  display: none;
}

/* Smaller screens */
.main-nav .tablet-hide {
  display: block;
}

/* Large Desktop */
@media (min-width: 1200px) {
  .logo img {
    height: 40px;
    margin-left: 80px;
  }
  
  .nav-container {
    margin-right: 80px;
  }
  
  .main-nav {
    margin-right: 20px;
  }

  .main-nav li {
    margin-left: 30px;
  }

  .main-nav a {
    font-size: 14px;
  }
  
  /* Desktop hamburger */
  .hamburger-nav .desktop-only {
    display: block;
  }
  
  .hamburger-nav .tablet-only,
  .hamburger-nav .mobile-only {
    display: none;
  }
}

/* Tablet Landscape */
@media (max-width: 1199px) and (min-width: 992px) {
  .logo img {
    height: 38px;
    margin-left: 40px;
  }
  
  .nav-container {
    margin-right: 40px;
  }

  .main-nav li {
    margin-left: 25px;
  }
  
  /* Main nav on larger tablets */
  .main-nav .tablet-hide {
    display: none !important;
  }
  
  /* Hamburger menu on larger tablets */
  .hamburger-nav .desktop-only {
    display: none !important;
  }
  
  .hamburger-nav .tablet-only {
    display: block !important;
  }
  
  .hamburger-nav .mobile-only {
    display: none !important;
  }

  .hamburger-nav {
    width: 280px;
    right: 0;
    top: 56px;
    height: calc(100vh - 56px);
    transform: translateX(100%);
    border-left: 1px solid #252424;
    border-top: none;
    box-shadow: -2px 0 10px rgba(0, 0, 0, 0.3);
  }

  .hamburger-nav.mobile-open {
    transform: translateX(0);
  }

  .hamburger-nav ul {
    padding: 40px 0 20px 0;
    text-align: left;
  }

  .hamburger-nav li {
    margin: 0;
  }

  .hamburger-nav a {
    font-size: 14px;
    padding: 16px 20px;
    margin: 0 20px;
    justify-content: flex-start;
    display: flex;
    align-items: center;
  }
}

/* Tablet Portrait */
@media (max-width: 991px) and (min-width: 769px) {
  .main-header {
    position: sticky;
    top: 0;
    width: 100vw;
    margin-left: calc(-50vw + 50%);
    margin-right: calc(-50vw + 50%);
    box-sizing: border-box;
  }

  .logo img {
    height: 36px;
    margin-left: 20px;
  }
  
  .nav-container {
    margin-right: 20px;
  }

  .main-nav li {
    margin-left: 15px;
  }

  .main-nav a {
    font-size: 12px;
  }

  /* Keep first 4 items in main nav */
  .main-nav .tablet-hide {
    display: none !important;
  }

  /* hamburger menu on tablet */
  .hamburger-nav .desktop-only {
    display: none !important;
  }

  .hamburger-nav .mobile-only {
    display: none !important;
  }

  .hamburger-nav .tablet-only {
    display: block !important;
  }

  .hamburger-nav {
    width: 280px;
    right: 0;
    top: 56px;
    height: calc(100vh - 56px);
    transform: translateX(100%);
    border-left: 1px solid #252424;
    border-top: none;
    box-shadow: -2px 0 10px rgba(0, 0, 0, 0.3);
  }

  .hamburger-nav.mobile-open {
    transform: translateX(0);
  }

  .hamburger-nav ul {
    padding: 40px 0 20px 0;
    text-align: left;
  }

  .hamburger-nav li {
    margin: 0;
  }

  .hamburger-nav a {
    font-size: 14px;
    padding: 16px 20px;
    margin: 0 20px;
    justify-content: flex-start;
    display: flex;
    align-items: center;
  }
}

/* Mobile Landscape */
@media (max-width: 768px) and (min-width: 481px) {
  .main-header {
    padding: 8px 0;
    min-height: 52px;
  }

  .logo img {
    margin-left: 30px;
    height: 34px;
  }

  .nav-container {
    margin-right: 30px;
  }

  .main-nav {
    display: none;
  }

  /* Mobile hamburger */
  .hamburger-nav .desktop-only,
  .hamburger-nav .tablet-only {
    display: none;
  }

  .hamburger-nav .mobile-only {
    display: block !important;
  }

  .hamburger-nav {
    width: 100%;
    max-width: 100vw;
    top: 52px;
    height: calc(100vh - 52px);
    transform: translateY(-100%);
    border-left: none;
    border-top: 1px solid #252424;
  }

  .hamburger-nav.mobile-open {
    transform: translateY(0);
  }

  .hamburger-nav ul {
    padding: 30px 0 40px 0;
    text-align: center;
  }

  .hamburger-nav li {
    margin: 8px 0;
  }

  .hamburger-nav a {
    font-size: 16px;
    padding: 14px 20px;
    margin: 0 30px;
    justify-content: center;
  }

  .hamburger-backdrop {
    top: 52px;
    height: calc(100vh - 52px);
  }
}

/* Mobile Portrait */
@media (max-width: 480px) {
  .main-header {
    padding: 6px 0;
    min-height: 48px;
  }

  .logo img {
    height: 32px;
    margin-left: 20px;
  }

  .nav-container {
    margin-right: 20px;
  }

  .main-nav {
    display: none;
  }

  /* Mobile nav */
  .hamburger-nav .desktop-only,
  .hamburger-nav .tablet-only {
    display: none;
  }

  .hamburger-nav .mobile-only {
    display: block !important;
  }

  .hamburger-nav {
    width: 100%;
    max-width: 100vw;
    top: 48px;
    height: calc(100vh - 48px);
  }

  .hamburger-nav ul {
    padding: 20px 0 30px 0;
  }

  .hamburger-nav li {
    margin: 6px 0;
  }

  .hamburger-nav a {
    font-size: 15px;
    padding: 12px 15px;
    margin: 0 20px;
    min-height: 40px;
  }

  .hamburger-backdrop {
    top: 48px;
    height: calc(100vh - 48px);
  }
}

/* Extra Small Mobile */
@media (max-width: 360px) {
  .logo img {
    height: 30px;
    margin-left: 15px;
  }

  .nav-container {
    margin-right: 15px;
  }

  .hamburger-menu-icon {
    width: 36px;
    height: 36px;
  }

  .hamburger-nav a {
    font-size: 14px;
    margin: 0 15px;
    padding: 10px 12px;
  }

  /* Extra small screens */
  .hamburger-nav .desktop-only,
  .hamburger-nav .tablet-only {
    display: none !important;
  }
  
  .hamburger-nav .mobile-only {
    display: block !important;
  }
}

/* Touch device optimizations */
@media (hover: none) and (pointer: coarse) {
  .main-nav a:hover,
  .hamburger-nav a:hover {
    background-color: transparent;
    text-decoration: none;
  }

  .main-nav a:active {
    text-decoration: underline;
    text-underline-offset: 4px;
  }

  .hamburger-nav a:active {
    background-color: #252424;
  }

  .hamburger-menu-icon:hover {
    background-color: transparent;
  }

  .hamburger-menu-icon:active {
    background-color: rgba(255, 255, 255, 0.1);
  }
}
</style>