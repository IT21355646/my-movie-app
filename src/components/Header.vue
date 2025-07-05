<template>
  <header class="main-header">
    <div class="logo">
      <img src="../assets/Logos/Logo White.svg" alt="Movie App Logo" />
    </div>
    <nav class="main-nav">
      <ul>
        <li><a href="#">HOME</a></li>
        <li><a href="#">OUR SCREENS</a></li>
        <li><a href="#">SCHEDULE</a></li>
        <li><a href="#">MOVIE LIBRARY</a></li>
        <li><a href="#">LOCATION & CONTACT</a></li>
      </ul>
    </nav>
    <nav class="hamburger-nav" :class="{ 'mobile-open': isMobileMenuOpen }">
      <ul>
        <li><a href="#">GALLERY</a></li>
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
    }
  }
};
</script>

<style lang="css" scoped>
.main-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 0 5px 0;
  background-color: #000;
  color: #fff;
  min-height: 60px; /* Ensures a consistent height */
  position: sticky;
  top: 0;
  z-index: 1000;
  border-bottom: 1px solid #252424; /* Add horizontal line */
  width: 100vw;
  margin-left: calc(-50vw + 50%);
}

.logo img {
  height: 40px; /* Adjust based on your logo size and design */
  margin-left: 40px; /* Add back some spacing from edge */
}

/* Desktop Navigation (default) */
.main-nav {
  margin-right: 10px; /* Reduced spacing from hamburger icon */
}

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
  font-weight: normal;
  font-size: 14px;
  padding: 5px 0;
  display: block;
  transition: text-decoration 0.3s ease; /* For hover effect */
  border-bottom: 2px solid transparent;
}

.main-nav a:hover {
  text-decoration: underline;
  text-underline-offset: 4px;
}

/* Hamburger Menu Icon */
.hamburger-menu-icon {
  display: flex; /* Show on both desktop and mobile */
  flex-direction: column;
  justify-content: space-around;
  width: 30px;
  height: 25px;
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 0;
  z-index: 1001; /* Above mobile menu */
  margin-right: 40px; /* Add margin to keep icon within bounds */
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

/* Hamburger Navigation (hidden by default, shown when toggled) */
.hamburger-nav {
  display: none;
  position: fixed; /* Changed back to fixed for better positioning */
  top: 71px; /* Below the header */
  right: 0;
  width: 300px; /* Increased width */
  max-width: calc(100vw - 20px); /* Ensure it doesn't exceed viewport */
  height: calc(100vh - 71px); /* Full height minus header */
  background-color: #000;
  border-left: 1px solid #252424;
  z-index: 999;
  opacity: 0;
  transform: translateX(100%);
  transition: all 0.3s ease-in-out;
  overflow-y: auto;
}

.hamburger-nav.mobile-open {
  display: block;
  opacity: 1;
  transform: translateX(0);
}

.hamburger-nav ul {
  list-style: none;
  margin: 0;
  padding: 20px 0;
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
  padding: 15px 20px;
  display: block;
  transition: background-color 0.3s ease;
}

.hamburger-nav a:hover {
  background-color: #252424;
  text-decoration: none;
}

/* Tablet and Mobile Styles */
@media (max-width: 768px) {
  .main-header {
    padding: 10px 0 5px 0; /* Remove horizontal padding */
  }

  .logo img {
    margin-left: 20px; /* Spacing from edge on mobile */
    height: 35px; /* Slightly smaller logo */
  }

  .main-nav {
    display: none; /* Hide desktop nav on mobile */
    margin-right: 10px; /* Keep consistent spacing */
  }

  .hamburger-menu-icon {
    margin-right: 20px; /* Reduced margin for mobile */
  }

  .hamburger-nav {
    width: 80%; /* Larger width on tablet/mobile */
    max-width: calc(100vw - 10px); /* Even smaller margin on mobile */
    top: 61px; /* Adjust for smaller header height */
    height: calc(100vh - 61px);
  }

  .hamburger-nav.mobile-open {
    display: flex;
    transform: translateX(0);
  }

  .hamburger-nav ul {
    text-align: center;
    padding: 0;
  }

  .hamburger-nav li {
    margin: 20px 0;
  }

  .hamburger-nav a {
    font-size: 24px;
    padding:5px 0;
  }

  .hamburger-nav a:hover {
    background-color: transparent;
    text-decoration: underline;
    text-underline-offset: 4px;
  }
}

/* Mobile-specific adjustments */
@media (max-width: 480px) {
  .main-header {
    padding: 10px 0;
  }

  .logo img {
    height: 32px; /* Even smaller logo for very small screens */
    margin-left: 15px; /* Minimal spacing from edge */
  }

  .hamburger-menu-icon {
    width: 25px; /* Slightly smaller hamburger icon */
    height: 20px;
    margin-right: 15px; /* Minimal margin for small screens */
  }

  .hamburger-nav {
    width: 90%; /* Almost full width on very small screens */
    max-width: calc(100vw - 5px); /* Minimal margin */
    top: 56px; /* Adjust for even smaller header */
    height: calc(100vh - 56px);
  }

  .hamburger-nav a {
    font-size: 16px;
    padding: 12px 15px;
  }
}
</style>