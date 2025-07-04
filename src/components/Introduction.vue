<template>
  <section class="introduction-section">
    <h2 class="section-title">MOVIE LIBRARY</h2>
    <p class="intro-text">
      Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua.
    </p>
  </section>
</template>

<script>
export default {
  name: 'AppIntroduction',
};
</script>

<style scoped>
.introduction-section {
  padding: 60px 20px; /* Adjust padding as per design */
  text-align: center; /* Center align content if needed based on design */
  max-width: 960px; /* Max width for content, adjust as needed */
  margin: 0 auto; /* Center the section on larger screens */
}

.section-title {
  font-size: 3em; /* Adjust font size as per design (e.g., Desktop.pdf) */
  color: #F0C000; /* Example color, use your design's color */
  margin-bottom: 20px;
  font-weight: bold;
  text-transform: uppercase; /* Match design if text is uppercase */
}

.intro-text {
  font-size: 1.2em; /* Adjust font size as per design */
  line-height: 1.6;
  color: #ccc; /* Lighter color for text */
  margin: 0 auto;
  max-width: 700px; /* Max width for text block */
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .introduction-section {
    padding: 40px 15px;
  }
  .section-title {
    font-size: 2.2em;
  }
  .intro-text {
    font-size: 1em;
  }
}

@media (max-width: 480px) {
  .introduction-section {
    padding: 30px 10px;
  }
  .section-title {
    font-size: 1.8em;
  }
  .intro-text {
    font-size: 0.9em;
  }
}
</style>