<template>
  <header class="main-header">
    <div class="logo">
      <img src="../assets/Logos/Logo White.svg" alt="Logoipsum" />
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
    <button class="hamburger-menu-icon" @click="toggleMobileMenu">
      &#9776; </button>
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
  methods: {
    toggleMobileMenu() {
      this.isMobileMenuOpen = !this.isMobileMenuOpen;
      // You'll implement the actual menu opening/closing logic later with CSS
    },
  },
};
</script>

<style lang="css" scoped>
/* Basic styles for the header (you'll expand on this for responsiveness) */
.main-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  background-color: #000; /* Dark background */
  color: #fff;
}

.logo img {
  height: 40px; /* Adjust as needed */
}

.main-nav ul {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex; /* For horizontal menu on desktop */
}

.main-nav li {
  margin-left: 20px;
}

.main-nav a {
  color: #fff;
  text-decoration: none;
  font-weight: bold;
  /* Add hover effect later */
}

.hamburger-menu-icon {
  display: none; /* Hidden by default on desktop, shown on mobile/tablet */
  background: none;
  border: none;
  color: #fff;
  font-size: 30px;
  cursor: pointer;
}

/* Media queries will be added later for responsiveness */
</style>