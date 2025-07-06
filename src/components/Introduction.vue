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
  font-size: 3em;
  margin: 0 0 10px 0;
  padding: 0;
  font-weight: normal;
  text-transform: uppercase;
  line-height: 1.4;
  font-family: 'Trebuchet MS', 'Lucida Grande', Arial, sans-serif; 
  letter-spacing: 0.05em; 
  font-stretch: expanded; 
}

.intro-text {
  font-size: 1.4em; 
  line-height: 1.3;
  color: #b4b4b4;
  max-width: 50%;
  margin: 0;
  padding: 0;
}

/* Responsive adjustments */
@media (max-width: 992px) {
  .content-container {
    margin-left: 60px;
    padding-left: 0;
  }
  
  .section-title {
    font-size: 2.5em;
  }
  
  .intro-text {
    font-size: 1.2em;
    max-width: 60%;
  }
}

@media (max-width: 768px) {
  .introduction-section {
    padding: 30px 0;
  }
  
  .content-container {
    margin-left: 40px;
    padding: 0;
  }
  
  .section-title {
    font-size: 2.2em;
  }
  
  .intro-text {
    font-size: 1.1em;
    max-width: 80%;
  }
}

@media (max-width: 480px) {
  .introduction-section {
    padding: 25px 0;
  }
  
  .content-container {
    margin-left: 20px;
    padding: 0;
    max-width: calc(100% - 40px);
  }
  
  .section-title {
    font-size: 1.8em;
  }
  
  .intro-text {
    font-size: 1em;
    max-width: 100%;
  }
}
</style>