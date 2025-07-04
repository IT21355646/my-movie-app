<template>
  <section class="movie-grid-section">
    <h2 class="section-title">Collect your favourites</h2>

    <div class="search-bar">
      <input type="text" placeholder="Q Search title and add to grid" class="search-input" />
    </div>

    <div class="movie-list">
      <div class="movie-item">
        <button class="close-button" @click="removeMovie(1)">X</button>
        <img src="../assets/Images/Batman.jpg" alt="Batman Returns Poster" class="movie-poster" />
        <h3 class="movie-title">Batman Returns</h3>
        <p class="movie-description">
          Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut.....
        </p>
      </div>

      <div class="movie-item">
        <button class="close-button" @click="removeMovie(2)">X</button>
        <img src="../assets/Images/Wild West.jpg" alt="Wild Wild West Poster" class="movie-poster" />
        <h3 class="movie-title">Wild Wild West</h3>
        <p class="movie-description">
          Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut.....
        </p>
      </div>

      <div class="movie-item">
        <button class="close-button" @click="removeMovie(3)">X</button>
        <img src="../assets/Images/Spiderman.jpg" alt="The Amazing Spiderman Poster" class="movie-poster" />
        <h3 class="movie-title">The Amazing Spiderman</h3>
        <p class="movie-description">
          Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut.....
        </p>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'AppMovieGrid',
  methods: {
    removeMovie(id) {
      console.log(`Movie with ID ${id} removed (placeholder for future functionality).`);
      // This will be implemented fully when we have dynamic movie data
    },
  },
};
</script>

<style scoped>
.movie-grid-section {
  padding: 60px 20px;
  max-width: 1200px; /* Adjust max width as per design */
  margin: 0 auto;
  text-align: center; /* For centering the title and search bar */
}

.section-title {
  font-size: 2.5em; /* Adjust as per design */
  color: #fff; /* White color for this title */
  margin-bottom: 40px; /* Spacing below title */
  font-weight: bold;
}

.search-bar {
  margin-bottom: 40px; /* Spacing below search bar */
}

.search-input {
  width: 100%;
  max-width: 400px; /* Adjust width as per design */
  padding: 12px 20px;
  border: 1px solid #F0C000; /* Border color from your design */
  border-radius: 5px;
  background-color: #222; /* Dark background for input */
  color: #fff;
  font-size: 1.1em;
  outline: none;
}

.search-input::placeholder {
  color: #aaa;
}

.movie-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); /* Flexible columns */
  gap: 30px; /* Spacing between movie items */
  justify-content: center;
}

.movie-item {
  background-color: #1a1a1a; /* Darker background for movie cards */
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  position: relative;
  padding-bottom: 20px; /* Padding for text content */
  text-align: left; /* Align text within card */
}

.movie-poster {
  width: 100%;
  height: 300px; /* Fixed height for posters, adjust as needed */
  object-fit: cover; /* Ensures images fill the space */
  display: block;
  border-bottom: 1px solid #333; /* Separator */
}

.movie-title {
  font-size: 1.5em;
  color: #F0C000; /* Title color */
  margin: 15px 15px 5px 15px; /* Spacing */
}

.movie-description {
  font-size: 0.95em;
  color: #ccc;
  margin: 0 15px 15px 15px;
  line-height: 1.5;
  min-height: 70px; /* Ensure consistent height for description */
  display: -webkit-box;
  -webkit-line-clamp: 4; /* Limit to 4 lines */
  -webkit-box-orient: vertical;
  overflow: hidden;
  text-overflow: ellipsis;
}

.close-button {
  position: absolute;
  top: 10px;
  right: 10px;
  background-color: #F0C000;
  color: #000;
  border: none;
  border-radius: 50%;
  width: 25px;
  height: 25px;
  font-size: 1em;
  font-weight: bold;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  line-height: 1; /* Adjust for vertical alignment */
  z-index: 5;
  transition: background-color 0.3s ease;
}

.close-button:hover {
  background-color: #e0b000;
}

/* Responsive adjustments for Movie Grid */
@media (max-width: 992px) { /* Tablet breakpoint - show 2 movies per row */
  .movie-list {
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); /* Adjust for 2 columns */
    max-width: 600px; /* Confine to max 2 columns width */
    margin: 0 auto;
  }
  .section-title {
    font-size: 2.2em;
  }
}

@media (max-width: 768px) { /* Even smaller tablet/large mobile */
  .movie-grid-section {
    padding: 40px 15px;
  }
  .movie-list {
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); /* Adjust for potentially 2 smaller columns */
    max-width: 480px; /* Example max width */
    margin: 0 auto;
  }
  .section-title {
    font-size: 2em;
  }
}

@media (max-width: 576px) { /* Mobile breakpoint - show 1 movie per row */
  .movie-list {
    grid-template-columns: 1fr; /* Single column */
    max-width: 320px; /* Confine to single column width */
    margin: 0 auto;
  }
  .movie-item {
    margin: 0 auto; /* Center single item */
  }
  .movie-poster {
    height: 250px; /* Adjust height for mobile */
  }
  .section-title {
    font-size: 1.8em;
    margin-bottom: 30px;
  }
  .search-input {
    max-width: 90%;
  }
}
</style>