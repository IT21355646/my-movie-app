<template>
  <div id="app">
    <AppHeader />
    <AppHero />
    <main>
      </main>
  </div>
</template>

<script>
import AppHeader from './components/Header.vue';
import AppHero from './components/Hero.vue'; // Import the new Hero component

export default {
  name: 'App',
  components: {
    AppHeader,
    AppHero, // Register the Hero component
  },
};
</script>

<style>
/* Global styles (e.g., body, font-family) */
body {
  margin: 0;
  font-family: Arial, sans-serif; /* Example font */
  background-color: #121212; /* Dark background for the whole app */
  color: #fff;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>