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
  display: flex;
  flex-direction: column;
  padding: 40px 0;
  background-color: #000;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
  width: 100vw;
  border-top: 1px solid #222121;
  margin: 0;
  box-sizing: border-box;
  position: relative;
  left: 50%;
  right: 50%;
  margin-left: -50vw;
  margin-right: -50vw;
}

.content-container {
  width: 100%;
  max-width: 1200px;
  margin: 0;
  padding: 0;
  text-align: left;
  margin-left: 80px;
  padding-left: 10px;
}

.section-title {
  font-size: 3em; /* Increased from 2.5em */
  margin: 0 0 10px 0;
  padding: 0;
  font-weight: normal;
  text-transform: uppercase;
  line-height: 1.4; /* Increased line height for taller letters */
  font-family: 'Trebuchet MS', 'Lucida Grande', Arial, sans-serif; /* Font with taller letter forms but not bold */
  letter-spacing: 0.05em; /* Slight letter spacing for better readability */
  font-stretch: expanded; /* Makes letters taller/wider without bold */
}

.intro-text {
  font-size: 1.4em; /* Increased from 1.2em */
  line-height: 1.3;
  color: #b4b4b4;
  max-width: 50%; /* Limit to 50% of page width */
  margin: 0;
  padding: 0;
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .introduction-section {
    padding: 30px 0;
  }
  .content-container {
    margin: 0;
    padding: 0;
  }
  .section-title {
    font-size: 2.2em; /* Increased from 1.8em */
  }
  .intro-text {
    font-size: 1.1em; /* Increased from 0.9em */
    max-width: 70%; /* Slightly wider on tablets */
  }
}

@media (max-width: 480px) {
  .introduction-section {
    padding: 25px 0;
  }
  .content-container {
    margin: 0;
    padding: 0;
  }
  .section-title {
    font-size: 1.5em; /* Increased from 1.2em */
  }
  .intro-text {
    font-size: 1em; /* Increased from 0.8em */
    max-width: 100%; /* Full width on mobile */
  }
}
</style>