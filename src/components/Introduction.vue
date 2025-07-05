<template>
  <section class="introduction-section">
    <div class="content-container">
      <h2 class="section-title">MOVIE LIBRARY</h2>
      <p class="intro-text">
        Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua.
      </p>
    </div>
  </section>
</template>

<script>
export default {
  name: 'AppIntroduction',
};
</script>

<style scoped>
.introduction-section {
  padding: 40px 0;
  background-color: #000;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
  width: 100%;
  border-top: 1px solid #222121;
}

.content-container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px 0 60px;
  text-align: left;
}

.section-title {
  font-size: 2.5em;
  margin-bottom: 10px;
  font-weight: normal;
  text-transform: uppercase;
}

.intro-text {
  font-size: 1.2em;
  line-height: 1.3;
  color: #908888;
  max-width: none;
  margin: 0;
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .introduction-section {
    padding: 30px 0;
  }
  .content-container {
    padding: 0 20px 0 40px;
  }
  .section-title {
    font-size: 1.8em;
  }
  .intro-text {
    font-size: 0.9em;
  }
}

@media (max-width: 480px) {
  .introduction-section {
    padding: 25px 0;
  }
  .content-container {
    padding: 0 15px 0 20px;
  }
  .section-title {
    font-size: 1.2em;
  }
  .intro-text {
    font-size: 0.8em;
  }
}
</style>