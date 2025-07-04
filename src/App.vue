<template>
  <div id="app">
    <AppHeader />
    <AppHero />
    <AppIntroduction />
    <AppMovieGrid /> <main>
      </main>
  </div>
</template>

<script>
import AppHeader from './components/Header.vue';
import AppHero from './components/Hero.vue';
import AppIntroduction from './components/Introduction.vue';
import AppMovieGrid from './components/MovieGrid.vue'; // Import the new component

export default {
  name: 'App',
  components: {
    AppHeader,
    AppHero,
    AppIntroduction,
    AppMovieGrid, // Register the component
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