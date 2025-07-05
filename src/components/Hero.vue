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
  width: 100vw;
  margin-left: calc(-50vw + 50%);
  position: relative;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
}

.hero-image {
  width: 100%;
  height: auto;
  display: block;
  object-fit: cover;
  object-position: bottom;
  min-height: 300px;
  max-height: 500px;
  transform: scale(1);
  transition: transform 0.3s ease;
}

/* Tablet */
@media (max-width: 992px) {
  .hero-image {
    min-height: 250px;
    max-height: 400px;
    transform: scale(1.1);
  }
}

/* Mobile Landscape */
@media (max-width: 768px) {
  .hero-image {
    min-height: 200px;
    max-height: 300px;
    transform: scale(1.2);
  }
}

/* Mobile Portrait */
@media (max-width: 480px) {
  .hero-image {
    min-height: 180px;
    max-height: 250px;
    transform: scale(2.5);
    object-position: bottom;
  }
}

/* Extra Small Mobile */
@media (max-width: 360px) {
  .hero-image {
    min-height: 160px;
    max-height: 220px;
    transform: scale(2.6);
    object-position: bottom;
  }
}
</style>