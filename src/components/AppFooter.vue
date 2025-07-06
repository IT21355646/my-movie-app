<template>
  <footer class="app-footer">
    <div class="footer-content-wrapper">
      <div class="footer-section copyright">
        <p>Copyight &copy; 2022 Amadeus Hotels. All rights reserved.</p>
      </div>

      <div class="footer-section attribution">
        <p>Photos by <a href="#" class="photo-link">Felix Maaneeram</a> & <a href="#" class="photo-link">Serge Kutuzov</a> on <a href="https://unsplash.com" class="photo-link">Unsplash</a></p>
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
  background-color: #1a1a1a;
  color: #b4b4b4;
  padding: 10px 10px;
  text-align: center;
  font-size: 1.0em;
  border-top: 1px solid #413d3d; /* Small separator from content above */
  width: 100vw;
  max-width: none;
  margin-left: calc(-50vw + 50%);
  box-sizing: border-box;
}

.footer-content-wrapper {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  max-width: none;
  margin: 0 auto;
  padding: 0 60px;
  box-sizing: border-box;
}

.footer-section {
  padding: 2px;
  flex-basis: 45%; /* Increase basis to give more space */
  min-width: 200px; /* Reduce minimum width */
  white-space: nowrap; /* Prevent text wrapping */
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

.photo-link {
  color: #b4b4b4;
  text-decoration: underline;
}

.photo-link:hover {
  color: #F0C000;
  text-decoration: underline;
}

/* Responsive adjustments */
@media (max-width: 992px) {
  .footer-content-wrapper {
    flex-direction: column;
    gap: 10px;
    padding: 0 40px;
  }

  .footer-section {
    flex-basis: 100%;
    width: 100%;
    text-align: center !important;
    white-space: normal;
  }

  .footer-section.copyright {
    text-align: center !important;
    margin-bottom: 5px;
  }

  .footer-section.attribution {
    text-align: center !important;
  }
}

@media (max-width: 768px) {
  .app-footer {
    padding: 20px 0;
  }
  
  .footer-content-wrapper {
    flex-direction: column;
    text-align: center;
    padding: 0 80px;
    gap: 1px;
  }

  .footer-section {
    flex-basis: 100%;
    text-align: center !important;
    margin-bottom: 0;
    min-width: auto;
    white-space: normal; /* Allow wrapping on mobile */
  }
  
  .social-icons {
    justify-content: center;
  }
}

@media (max-width: 480px) {
  .app-footer {
    padding: 15px 0;
  }
  
  .footer-content-wrapper {
    padding: 0 40px;
    gap: 1px;
  }
  
  .footer-section p {
    font-size: 1.1em;
    line-height: 1.4;
  }
  
  .footer-section h3 {
    font-size: 1em;
    margin-bottom: 10px;
  }
  
  .social-icon {
    width: 30px;
    height: 30px;
    font-size: 1.2em;
  }
}
</style>