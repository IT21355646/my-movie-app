<template>
  <div id="app">
    <AppHeader />
    <AppHero />
    <AppIntroduction />
    <AppMovieGrid />
    <AppContactUs />
    <AppFooter />
  </div>
</template>

<script>
import AppHeader from './components/Header.vue';
import AppHero from './components/Hero.vue';
import AppIntroduction from './components/Introduction.vue';
import AppMovieGrid from './components/MovieGrid.vue';
import AppContactUs from './components/ContactUs.vue';
import AppFooter from './components/AppFooter.vue';

export default {
  name: 'App',
  components: {
    AppHeader,
    AppHero,
    AppIntroduction,
    AppMovieGrid,
    AppContactUs,
    AppFooter,
  },
};
</script>

<style>
/* Global styles */
body {
  margin: 0;
  font-family: Arial, sans-serif; 
  background-color: #121212; /* Dark background for the whole app */
  color: #fff;
  
  position: relative;
  overflow-x: hidden;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>