<template>
  <section class="movie-grid-section">
    <div class="header-row">
      <h2 class="section-title">Collect your favourites</h2>
      <div class="search-bar">
        <div class="search-input-container">
          <img src="../assets/Icons/Search White.svg" alt="Search" class="search-icon" />
          <input
            type="text"
            v-model="searchQuery"
            @input="searchMovies"
            placeholder="Search title and add to grid"
            class="search-input"
          />
        </div>
      </div>
    </div>

    <div class="movie-list">
      <div
        v-for="movie in movies"
        :key="movie.id"
        class="movie-item"
      >
        <button class="close-button" @click="removeMovie(movie.id)">
          <img src="../assets/Icons/Close Grey.svg" alt="Close" class="close-icon" />
        </button>
        <img
          :src="getMoviePosterUrl(movie.poster_path)"
          :alt="movie.title + ' Poster'"
          class="movie-poster"
        />
        <h3 class="movie-title">{{ movie.title }}</h3>
        <p class="movie-description">
          {{ movie.overview || 'No description available.' }}
        </p>
      </div>
      <p v-if="movies.length === 0 && !loading" class="no-movies-message">
        No movies to display. Try searching for some!
      </p>
      <p v-if="loading" class="loading-message">Loading movies...</p>
      <p v-if="error" class="error-message">{{ error }}</p>
    </div>
  </section>
</template>

<script>
import { ref, onMounted } from 'vue';

export default {
  name: 'AppMovieGrid',
  setup() {
    const movies = ref([]);
    const searchQuery = ref('');
    const loading = ref(false);
    const error = ref(null);

    // !! IMPORTANT: Replace 'YOUR_API_KEY' with your actual TMDb API key !!
    const API_KEY = '5019f2f7d1451fe858585b1af68d2ac0';
    const BASE_URL = 'https://api.themoviedb.org/3';
    const IMAGE_BASE_URL = 'https://image.tmdb.org/t/p/w500'; // Common poster size

    const fetchInitialMovies = async () => {
      loading.value = true;
      error.value = null;
      try {
        // Using a common endpoint for popular movies
        const response = await fetch(`${BASE_URL}/movie/popular?api_key=${API_KEY}&language=en-US&page=1`);
        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }
        const data = await response.json();
        // Take the first 3 movies as initial
        movies.value = data.results.slice(0, 3);
      } catch (e) {
        error.value = `Failed to fetch initial movies: ${e.message}. Please check your API key and network connection.`;
        console.error('Error fetching initial movies:', e);
      } finally {
        loading.value = false;
      }
    };

    const searchMovies = async () => {
      if (searchQuery.value.length < 3) { // Only search if query is at least 3 characters
        // Clear search results if query is too short, but keep existing movies
        return;
      }

      loading.value = true;
      error.value = null;
      try {
        const response = await fetch(`${BASE_URL}/search/movie?api_key=${API_KEY}&language=en-US&query=${encodeURIComponent(searchQuery.value)}&page=1`);
        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }
        const data = await response.json();
        // To add movies to the grid while keeping existing movies, we'll merge them.
        // Filter out duplicates based on movie ID before adding.
        const newMovies = data.results.filter(
          (newMovie) => !movies.value.some((existingMovie) => existingMovie.id === newMovie.id)
        ).slice(0, 3); // Add up to 3 new movies from search

        // Concatenate new movies to the existing list
        movies.value = [...movies.value, ...newMovies];

      } catch (e) {
        error.value = `Failed to search movies: ${e.message}.`;
        console.error('Error searching movies:', e);
      } finally {
        loading.value = false;
      }
    };


    const removeMovie = (id) => {
      movies.value = movies.value.filter((movie) => movie.id !== id);
    };

    const getMoviePosterUrl = (posterPath) => {
      return posterPath ? `${IMAGE_BASE_URL}${posterPath}` : 'https://via.placeholder.com/150x225/202020/FFFFFF?text=No+Image';
    };

    onMounted(fetchInitialMovies); // Fetch movies when the component is mounted

    return {
      movies,
      searchQuery,
      loading,
      error,
      removeMovie,
      searchMovies,
      getMoviePosterUrl,
    };
  },
};
</script>

<style scoped>
.movie-grid-section {
  display: flex;
  flex-direction: column;
  padding: 40px 0;
  width: 100vw;
  min-height: 100vh;
  margin: 0;
  box-sizing: border-box;
  text-align: center;
  background-color: #1d1d1d;
  position: relative;
  left: 50%;
  right: 50%;
  margin-left: -50vw;
  margin-right: -50vw;
}

.header-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 30px;
  padding: 0 20px 20px 20px;
  position: relative;
}

.header-row::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 20px;
  right: 20px;
  height: 1px;
  background-color: #ffffff;
}

.section-title {
  font-size: 1.8em;
  color: #fff;
  margin: 0;
  font-weight: bold;
  text-align: left;
  line-height: 1.2;
}

.search-bar {
  margin: 0;
  padding: 0;
  flex-shrink: 0;
}

.search-input-container {
  position: relative;
  width: 100%;
  max-width: 280px;
}

.search-icon {
  position: absolute;
  left: 12px;
  top: 50%;
  transform: translateY(-50%);
  width: 16px;
  height: 16px;
  pointer-events: none;
  z-index: 1;
}

.search-input {
  width: 100%;
  padding: 10px 15px 10px 38px;
  border: 1px solid #ffffff;
  border-radius: 5px;
  background-color: #222;
  color: #fff;
  font-size: 0.9em;
  outline: none;
  box-sizing: border-box;
}

.search-input::placeholder {
  color: #aaa;
  font-size: 0.85em;
}

.movie-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
  justify-content: center;
  padding: 0 20px;
}

.movie-item {
  background-color: #3c3c3c;
  overflow: hidden;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  position: relative;
  padding-bottom: 15px;
  text-align: left;
  border-radius: 8px;
  transition: transform 0.3s ease, box-shadow 0.3s ease, background-color 0.3s ease;
  animation: fadeInUp 0.6s ease-out;
}

.movie-item:hover {
  transform: translateY(-8px) scale(1.02);
  box-shadow: 0 12px 24px rgba(0, 0, 0, 0.4);
  background-color: #454545;
}

.movie-poster {
  width: 100%;
  height: 280px;
  object-fit: cover;
  display: block;
  border-bottom: 1px solid #333;
  transition: transform 0.3s ease, filter 0.3s ease;
}

.movie-item:hover .movie-poster {
  transform: scale(1.05);
  filter: brightness(1.1);
}

.movie-title {
  font-size: 1.2em;
  margin: 12px 12px 8px 12px;
  line-height: 1.3;
  color: #fff;
  transition: color 0.3s ease;
}

.movie-item:hover .movie-title {
  color: #e0b000;
}

.movie-description {
  font-size: 0.85em;
  color: #ccc;
  margin: 0 12px 12px 12px;
  line-height: 1.4;
  min-height: 60px;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
  text-overflow: ellipsis;
  transition: color 0.3s ease;
}

.movie-item:hover .movie-description {
  color: #ffffff;
}

.close-button {
  position: absolute;
  top: 8px;
  right: 8px;
  background-color: rgba(26, 26, 28, 0.9);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  color: #000;
  border: none;
  border-radius: 4px;
  width: 36px;
  height: 36px;
  font-size: 1em;
  font-weight: bold;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  line-height: 1;
  z-index: 5;
  transition: all 0.3s ease;
  opacity: 0;
  transform: scale(0.8);
}

.movie-item:hover .close-button {
  opacity: 1;
  transform: scale(1);
}

.close-icon {
  width: 10px;
  height: 10px;
  transition: transform 0.3s ease;
}

.close-button:hover {
  background-color: #e0b000;
  transform: scale(1.1);
}

.close-button:hover .close-icon {
  transform: rotate(90deg);
}

.close-button:active {
  transform: scale(0.95);
}

/* Animation keyframes */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes pulse {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.05);
  }
}

/* Loading animation for new movies */
.movie-item.loading {
  animation: pulse 1.5s infinite;
}

/* Stagger animation for multiple items */
.movie-item:nth-child(1) { animation-delay: 0s; }
.movie-item:nth-child(2) { animation-delay: 0.1s; }
.movie-item:nth-child(3) { animation-delay: 0.2s; }
.movie-item:nth-child(4) { animation-delay: 0.3s; }
.movie-item:nth-child(5) { animation-delay: 0.4s; }
.movie-item:nth-child(6) { animation-delay: 0.5s; }

.no-movies-message, .loading-message, .error-message {
  color: #fff;
  font-size: 1em;
  margin-top: 30px;
  padding: 0 20px;
}

.error-message {
  color: #ff6b6b;
}

/* Large Desktop */
@media (min-width: 1200px) {
  .movie-grid-section {
    padding: 60px 0;
  }

  .header-row {
    padding: 0 80px 20px 80px;
    margin-bottom: 40px;
  }

  .header-row::after {
    left: 80px;
    right: 80px;
  }

  .section-title {
    font-size: 2.5em;
  }

  .search-input-container {
    max-width: 350px;
  }

  .search-icon {
    left: 15px;
    width: 18px;
    height: 18px;
  }

  .search-input {
    padding: 12px 20px 12px 45px;
    font-size: 1.1em;
  }

  .movie-list {
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 30px;
    padding: 0 80px;
  }

  .movie-poster {
    height: 380px;
  }

  .movie-title {
    font-size: 1.5em;
    margin: 15px 15px 5px 15px;
  }

  .movie-description {
    font-size: 1em;
    margin: 0 15px 15px 15px;
    min-height: 90px;
    -webkit-line-clamp: 4;
  }

  .close-button {
    top: 10px;
    right: 10px;
    width: 50px;
    height: 50px;
  }

  .close-icon {
    width: 12px;
    height: 12px;
  }

  .search-bar {
    margin: 0;
  }
}

/* Desktop */
@media (min-width: 992px) and (max-width: 1199px) {
  .movie-grid-section {
    padding: 50px 0;
  }

  .header-row {
    padding: 0 60px 20px 60px;
    margin-bottom: 35px;
  }

  .header-row::after {
    left: 60px;
    right: 60px;
  }

  .section-title {
    font-size: 2.2em;
  }

  .search-input-container {
    max-width: 320px;
  }

  .movie-list {
    grid-template-columns: repeat(auto-fit, minmax(230px, 1fr));
    gap: 25px;
    padding: 0 60px;
  }

  .movie-poster {
    height: 340px;
  }

  .movie-title {
    font-size: 1.3em;
    margin: 14px 14px 6px 14px;
  }

  .movie-description {
    font-size: 0.95em;
    margin: 0 14px 14px 14px;
    min-height: 80px;
  }

  .close-button {
    width: 44px;
    height: 44px;
  }

  .search-bar {
    margin: 0;
  }
}

/* Tablet Portrait */
@media (min-width: 769px) and (max-width: 991px) {
  .movie-grid-section {
    padding: 40px 0;
  }

  .header-row {
    padding: 0 40px 20px 40px;
    margin-bottom: 30px;
  }

  .header-row::after {
    left: 40px;
    right: 40px;
  }

  .section-title {
    font-size: 2em;
  }

  .search-input-container {
    max-width: 300px;
  }

  .movie-list {
    grid-template-columns: repeat(2, 1fr);
    gap: 20px;
    padding: 0 40px;
    max-width: 800px;
    margin: 0 auto;
  }

  .movie-poster {
    height: 320px;
  }

  .movie-title {
    font-size: 1.25em;
  }

  .movie-description {
    font-size: 0.9em;
    margin: 0 15px 15px 15px;
    min-height: 90px;
    -webkit-line-clamp: 4;
  }

  .close-button {
    width: 40px;
    height: 40px;
  }

  .search-bar {
    margin: 0;
  }
}

/* Mobile Landscape & Small Tablet */
@media (min-width: 481px) and (max-width: 768px) {
  .movie-grid-section {
    padding: 35px 0;
  }

  .header-row {
    flex-direction: column;
    align-items: flex-start;
    gap: 15px;
    padding: 0 30px 20px 30px;
    margin-bottom: 25px;
  }

  .header-row::after {
    left: 30px;
    right: 30px;
  }

  .section-title {
    font-size: 1.8em;
    width: 100%;
  }

  .search-bar {
    width: 100%;
    margin: 0;
  }

  .search-input-container {
    max-width: 100%;
  }

  .movie-list {
    grid-template-columns: repeat(2, 1fr);
    gap: 18px;
    padding: 0 30px;
  }

  .movie-poster {
    height: 300px;
  }

  .movie-title {
    font-size: 1.2em;
    margin: 12px 12px 8px 12px;
  }

  .movie-description {
    font-size: 0.85em;
    margin: 0 12px 12px 12px;
    min-height: 65px;
  }

  .close-button {
    width: 38px;
    height: 38px;
    top: 8px;
    right: 8px;
  }

  .close-icon {
    width: 10px;
    height: 10px;
  }
}

/* Mobile Portrait */
@media (max-width: 480px) {
  .movie-grid-section {
    padding: 30px 0;
  }

  .header-row {
    flex-direction: column;
    align-items: flex-start;
    gap: 15px;
    padding: 0 20px 15px 20px;
    margin-bottom: 20px;
  }

  .header-row::after {
    left: 20px;
    right: 20px;
  }

  .section-title {
    font-size: 1.6em;
    width: 100%;
    text-align: left;
  }

  .search-bar {
    width: 100%;
    margin: 0;
  }

  .search-input-container {
    max-width: 100%;
  }

  .search-input {
    padding: 12px 15px 12px 38px;
    font-size: 0.95em;
  }

  .search-input::placeholder {
    font-size: 0.9em;
  }

  .movie-list {
    grid-template-columns: 1fr;
    gap: 15px;
    padding: 0 20px;
  }

  .movie-item {
    max-width: 100%;
    margin: 0 auto;
  }

  .movie-poster {
    height: 280px;
  }

  .movie-title {
    font-size: 1.1em;
    margin: 10px 10px 6px 10px;
    text-align: left;
  }

  .movie-description {
    font-size: 0.8em;
    margin: 0 10px 10px 10px;
    min-height: 50px;
    -webkit-line-clamp: 3;
    text-align: left;
  }

  .close-button {
    width: 36px;
    height: 36px;
    top: 6px;
    right: 6px;
  }

  .close-icon {
    width: 9px;
    height: 9px;
  }

  .no-movies-message, .loading-message, .error-message {
    font-size: 0.95em;
    margin-top: 20px;
  }
}

/* Extra Small Mobile */
@media (max-width: 360px) {
  .section-title {
    font-size: 1.4em;
    text-align: left;
  }

  .search-input {
    font-size: 0.9em;
    padding: 10px 12px 10px 35px;
  }

  .search-icon {
    left: 10px;
    width: 14px;
    height: 14px;
  }

  .movie-poster {
    height: 250px;
  }

  .movie-title {
    font-size: 1em;
    margin: 8px 8px 5px 8px;
  }

  .movie-description {
    font-size: 0.75em;
    margin: 0 8px 8px 8px;
    min-height: 45px;
  }

  .close-button {
    width: 32px;
    height: 32px;
  }

  .close-icon {
    width: 8px;
    height: 8px;
  }
}

/* Touch device optimizations */
@media (hover: none) and (pointer: coarse) {
  .movie-item:hover {
    transform: none;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    background-color: #3c3c3c;
  }

  .movie-item:hover .movie-poster {
    transform: none;
    filter: none;
  }

  .movie-item:hover .movie-title {
    color: #fff;
  }

  .movie-item:hover .movie-description {
    color: #ccc;
  }

  .close-button {
    opacity: 1;
    transform: scale(1);
  }

  .close-button:hover {
    background-color: rgba(26, 26, 28, 0.9);
    transform: scale(1);
  }

  .close-button:active {
    background-color: #e0b000;
    transform: scale(0.95);
  }

  .movie-item {
    transition: transform 0.2s ease;
  }

  .movie-item:active {
    transform: scale(0.98);
  }
}
</style>