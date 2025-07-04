<template>
  <footer class="app-footer">
    <div class="footer-content-wrapper">
      <div class="footer-section copyright">
        <p>&copy; 2022 Amadeus Hotels. All rights reserved.</p>
      </div>

      <div class="footer-section social-media">
        <h3>Follow us on</h3>
        <div class="social-icons">
          <a href="#" class="social-icon" aria-label="Facebook"><i class="fab fa-facebook-f">F</i></a>
          <a href="#" class="social-icon" aria-label="Twitter"><i class="fab fa-twitter">T</i></a>
          <a href="#" class="social-icon" aria-label="Instagram"><i class="fab fa-instagram">I</i></a>
        </div>
      </div>

      <div class="footer-section attribution">
        <p>Photos by Felix Maaneeram & Serge Kutuzov on Unsplash</p>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'AppFooter',
};
</script>

<style scoped>
.app-footer {
  background-color: #0d0d0d; /* Darker background for footer */
  color: #ccc;
  padding: 40px 20px;
  text-align: center;
  font-size: 0.9em;
  border-top: 1px solid #222; /* Small separator from content above */
}

.footer-content-wrapper {
  display: flex;
  flex-wrap: wrap; /* Allow wrapping on smaller screens */
  justify-content: space-between; /* Distribute items horizontally */
  align-items: center; /* Vertically align items */
  max-width: 1200px;
  margin: 0 auto;
}

.footer-section {
  padding: 10px;
  flex-basis: 30%; /* Roughly distribute space */
  min-width: 250px; /* Minimum width before stacking */
}

.footer-section.copyright {
  text-align: left;
}

.footer-section.social-media {
  text-align: center;
}

.footer-section.attribution {
  text-align: right;
}

.footer-section h3 {
  color: #fff;
  font-size: 1.1em;
  margin-bottom: 15px;
}

.social-icons {
  display: flex;
  justify-content: center;
  gap: 15px; /* Space between icons */
}

.social-icon {
  color: #ccc;
  font-size: 1.5em; /* Adjust icon size */
  transition: color 0.3s ease;
  text-decoration: none; /* Remove underline from links */
  /* Basic styling for placeholder text icons */
  border: 1px solid #ccc;
  border-radius: 50%;
  width: 35px;
  height: 35px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: bold;
}

.social-icon:hover {
  color: #F0C000; /* Accent color on hover */
  border-color: #F0C000;
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .footer-content-wrapper {
    flex-direction: column; /* Stack sections vertically */
    text-align: center;
  }

  .footer-section {
    flex-basis: 100%; /* Take full width */
    text-align: center !important; /* Override specific alignment */
    margin-bottom: 20px; /* Add spacing between stacked sections */
  }

  .footer-section:last-child {
    margin-bottom: 0;
  }
}

@media (max-width: 480px) {
  .app-footer {
    padding: 30px 15px;
  }
  .footer-section p {
    font-size: 0.85em;
  }
}
</style>