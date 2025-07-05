<template>
  <section class="movie-grid-section">
    <div class="header-row">
      <h2 class="section-title">Collect your favourites</h2>
      <div class="search-bar">
        <input
          type="text"
          v-model="searchQuery"
          @input="searchMovies"
          placeholder="Q Search title and add to grid"
          class="search-input"
        />
      </div>
    </div>

    <div class="movie-list">
      <div
        v-for="movie in movies"
        :key="movie.id"
        class="movie-item"
      >
        <button class="close-button" @click="removeMovie(movie.id)">X</button>
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
  padding: 60px 0;
  width: 100vw; /* Full viewport width */
  min-height: 100vh; /* Full viewport height */
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
  margin-bottom: 40px;
  padding: 0 80px; /* Changed from 0 20px */
}

.section-title {
  font-size: 2.5em; /* Adjust as per design */
  color: #fff; /* White color for this title */
  margin: 0;
  font-weight: bold;
  text-align: left;
}

.search-bar {
  margin: 0;
  padding: 0;
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
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 30px;
  justify-content: center;
  padding: 0 80px; /* Changed from 0 20px */
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

.no-movies-message, .loading-message, .error-message {
  color: #fff;
  font-size: 1.2em;
  margin-top: 30px;
}

.error-message {
    color: #ff6b6b; /* Red color for error messages */
}


/* Responsive adjustments for Movie Grid */
@media (max-width: 992px) {
  .movie-list {
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    max-width: none;
    margin: 0 auto;
    padding: 0 60px; /* Reduced from 80px for tablets */
  }
  .section-title {
    font-size: 2.2em;
  }
  .header-row {
    padding: 0 60px; /* Reduced from 80px for tablets */
  }
}

@media (max-width: 768px) {
  .movie-grid-section {
    padding: 40px 0;
  }
  .movie-list {
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    max-width: none;
    margin: 0 auto;
    padding: 0 40px; /* Reduced from 80px for mobile */
  }
  .section-title {
    font-size: 2em;
  }
  .header-row {
    flex-direction: column;
    align-items: flex-start;
    gap: 20px;
    padding: 0 40px; /* Reduced from 80px for mobile */
  }
  .search-bar {
    width: 100%;
  }
}

@media (max-width: 576px) {
  .movie-list {
    grid-template-columns: 1fr;
    max-width: none;
    margin: 0 auto;
    padding: 0 20px; /* Reduced from 80px for small mobile */
  }
  .movie-item {
    margin: 0 auto;
  }
  .movie-poster {
    height: 250px;
  }
  .section-title {
    font-size: 1.8em;
  }
  .search-input {
    max-width: 100%;
  }
  .header-row {
    padding: 0 20px; /* Reduced from 80px for small mobile */
  }
}
</style>