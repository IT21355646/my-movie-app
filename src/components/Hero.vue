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
  object-position: bottom; 
  min-height: 300px; /* Reduced minimum height */
  max-height: 500px; /* Reduced maximum height */
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .hero-image {
    min-height: 180px;
    max-height: 350px;
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
    min-height: 150px;
    max-height: 250px;
  }
}
</style>