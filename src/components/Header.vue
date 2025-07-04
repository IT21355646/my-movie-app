<template>
  <header class="main-header">
    <div class="logo">
      <img src="../assets/Logos/Logo White.svg" alt="Movie App Logo" />
    </div>
    <nav class="main-nav" :class="{ 'mobile-open': isMobileMenuOpen }">
      <ul>
        <li><a href="#" @mouseover="applyHoverEffect" @mouseleave="removeHoverEffect">HOME</a></li>
        <li><a href="#" @mouseover="applyHoverEffect" @mouseleave="removeHoverEffect">OUR SCREENS</a></li>
        <li><a href="#" @mouseover="applyHoverEffect" @mouseleave="removeHoverEffect">SCHEDULE</a></li>
        <li><a href="#" @mouseover="applyHoverEffect" @mouseleave="removeHoverEffect">MOVIE LIBRARY</a></li>
        <li><a href="#" @mouseover="applyHoverEffect" @mouseleave="removeHoverEffect">LOCATION & CONTACT</a></li>
      </ul>
    </nav>
    <button class="hamburger-menu-icon" :class="{ 'active': isMobileMenuOpen }" @click="toggleMobileMenu">
      <span class="bar"></span>
      <span class="bar"></span>
      <span class="bar"></span>
    </button>
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
  mounted() {
    // Add event listener to close mobile menu on resize to desktop size
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
      // Close mobile menu if window is resized to desktop width (e.g., > 768px)
      if (window.innerWidth > 768 && this.isMobileMenuOpen) {
        this.isMobileMenuOpen = false;
        document.body.style.overflow = ''; // Re-enable scrolling
      }
    },
    applyHoverEffect(event) {
      event.target.style.color = '#F0C000'; /* Example hover color */
      event.target.style.transition = 'color 0.3s ease';
    },
    removeHoverEffect(event) {
      event.target.style.color = '#fff';
    }
  }
};
</script>

<style lang="css" scoped>
.main-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px 20px; /* Adjust padding as per design */
  background-color: #000;
  color: #fff;
  min-height: 60px; /* Ensures a consistent height */
  position: sticky;
  top: 0;
  z-index: 1000;
}

.logo img {
  height: 40px; /* Adjust based on your logo size and design */
}

/* Desktop Navigation (default) */
.main-nav ul {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
}

.main-nav li {
  margin-left: 30px; /* Spacing between menu items */
}

.main-nav a {
  color: #fff;
  text-decoration: none;
  font-weight: bold;
  font-size: 16px;
  padding: 5px 0;
  display: block;
  transition: color 0.3s ease; /* For hover effect */
}

.main-nav a:hover {
  color: #F0C000; /* Example hover color */
}

/* Hamburger Menu Icon */
.hamburger-menu-icon {
  display: none; /* Hidden by default on desktop */
  flex-direction: column;
  justify-content: space-around;
  width: 30px;
  height: 25px;
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 0;
  z-index: 1001; /* Above mobile menu */
}

.hamburger-menu-icon .bar {
  width: 100%;
  height: 3px;
  background-color: #fff;
  border-radius: 5px;
  transition: all 0.3s ease-in-out;
}

/* Styles for animating hamburger icon into an 'X' */
.hamburger-menu-icon.active .bar:nth-child(1) {
  transform: translateY(11px) rotate(45deg);
}
.hamburger-menu-icon.active .bar:nth-child(2) {
  opacity: 0;
}
.hamburger-menu-icon.active .bar:nth-child(3) {
  transform: translateY(-11px) rotate(-45deg);
}

/* Tablet and Mobile Styles */
@media (max-width: 768px) { /* Adjust breakpoint as needed for tablet */
  .main-nav {
    display: none; /* Hide desktop nav by default on smaller screens */
    flex-direction: column;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.95); /* Semi-transparent overlay */
    justify-content: center;
    align-items: center;
    z-index: 999;
    transform: translateX(100%); /* Start off-screen */
    transition: transform 0.3s ease-in-out;
  }

  .main-nav.mobile-open {
    display: flex; /* Show when mobile menu is open */
    transform: translateX(0); /* Slide in */
  }

  .main-nav ul {
    flex-direction: column;
    text-align: center;
  }

  .main-nav li {
    margin: 20px 0; /* Spacing for vertical menu items */
  }

  .main-nav a {
    font-size: 24px; /* Larger font for mobile menu */
  }

  .hamburger-menu-icon {
    display: flex; /* Show hamburger icon on smaller screens */
  }
}

/* Mobile-specific adjustments (e.g., smaller padding or font sizes) */
@media (max-width: 480px) { /* Adjust breakpoint as needed for mobile */
  .main-header {
    padding: 10px 15px;
  }

  .logo img {
    height: 35px;
  }

  .main-nav a {
    font-size: 20px;
  }
}
</style>