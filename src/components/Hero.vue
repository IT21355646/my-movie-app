<template>
  <section class="hero-section">
    <img src="../assets/Images/Header Image.jpg" alt="Hero Image" class="hero-image" />
    </section>
</template>

<script>
export default {
  name: 'AppHero',
};
</script>

<style scoped>
.hero-section {
  width: 100%;
  position: relative; /* Needed for positioning content or overlays */
  overflow: hidden; /* Ensures image doesn't overflow */
}

.hero-image {
  width: 100%;
  height: auto; /* Maintain aspect ratio */
  display: block; /* Remove extra space below image */
  object-fit: cover; /* Crop image to cover the container */
  min-height: 300px; /* Minimum height for smaller screens, adjust as needed */
  max-height: 700px; /* Maximum height for larger screens, adjust as needed */
}

/* Example for content overlay if needed later */
/*
.hero-content {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  color: #fff;
  z-index: 10;
}

.hero-content h1 {
  font-size: 3em;
  margin-bottom: 10px;
}

.hero-content p {
  font-size: 1.2em;
}
*/

/* Responsive adjustments */
@media (max-width: 768px) {
  .hero-image {
    min-height: 250px;
    max-height: 500px;
  }
  /*
  .hero-content h1 {
    font-size: 2em;
  }
  .hero-content p {
    font-size: 1em;
  }
  */
}

@media (max-width: 480px) {
  .hero-image {
    min-height: 200px;
    max-height: 400px;
  }
}
</style>