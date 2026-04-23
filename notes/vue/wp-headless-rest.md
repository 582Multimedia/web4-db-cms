# Headless WP REST API

## MovieGallery.vue

Add a file called `MovieGallery.vue` and use the following code:

```html
<script setup>
// --- Configuration ---
const auth = btoa('username:application_password'); 
const baseUrl = 'https://your-site.com/wp-json/wp/v2';

import { ref, onMounted } from 'vue';

const movies = ref([]);
const isFetching = ref(true);
const errorMessage = ref('');

/**
 * Fetch all movies for the gallery
 */
const fetchMovies = async () => {
  isFetching.value = true;
  try {
    const res = await fetch(`${baseUrl}/movies?per_page=50&_fields=id,title,acf`, {
      headers: { 'Authorization': `Basic ${auth}` }
    });
    
    if (!res.ok) throw new Error("Could not sync with movie library.");
    
    movies.value = await res.json();
  } catch (err) {
    errorMessage.value = err.message;
  } finally {
    isFetching.value = false;
  }
};

onMounted(fetchMovies);
</script>

<template>
  <div class="component-container">
    <header class="gallery-header">
      <h2 class="main-title">Movie Gallery</h2>
      <p class="subtitle">Browse the complete collection of titles and synopses.</p>
    </header>

    <div v-if="isFetching" class="status-msg">
      <div class="spinner"></div>
      <p>Loading collection...</p>
    </div>

    <div v-else-if="errorMessage" class="status-bar error">
      {{ errorMessage }}
    </div>

    <div v-else class="movie-grid">
      <div v-for="movie in movies" :key="movie.id" class="movie-card">
        <div class="poster-frame">
          <div 
            v-if="movie.acf.poster" 
            v-html="movie.acf.poster.simple_value_formatted" 
            class="poster-html"
          ></div>
          <div v-else class="poster-placeholder">
            <span>No Poster Available</span>
          </div>
        </div>

        <div class="movie-meta">
          <h3 class="movie-title">{{ movie.title.rendered }}</h3>
          <span class="movie-year" v-if="movie.acf.year">
            {{ movie.acf.year.simple_value_formatted }}
          </span>
          <p class="movie-synopsis" v-if="movie.acf.synopsis">
            {{ movie.acf.synopsis.simple_value_formatted }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.component-container { 
  max-width: 1200px; 
  margin: 3rem auto; 
  padding: 2.5rem; 
  background: #fff; 
  border-radius: 16px; 
  border: 1px solid #e1e8ed; 
  box-shadow: 0 10px 25px rgba(0,0,0,0.05); 
  font-family: 'Inter', sans-serif; 
}

.gallery-header { margin-bottom: 3rem; }

.main-title { 
  font-size: 1.75rem; 
  font-weight: 800; 
  color: #1a202c; 
  margin-bottom: 0.5rem; 
  border-bottom: 2px solid #edf2f7; 
  padding-bottom: 1rem; 
}

.subtitle { color: #718096; font-size: 1rem; }

/* Grid Layout */
.movie-grid { 
  display: grid; 
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); 
  gap: 2rem; 
}

.movie-card { 
  background: #fff; 
  border-radius: 12px; 
  border: 1px solid #e2e8f0; 
  overflow: hidden; 
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.movie-card:hover { 
  transform: translateY(-8px); 
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
}

/* Poster Styling */
.poster-frame { 
  width: 100%; 
  height: 400px; 
  background: #f1f5f9; 
  position: relative;
}

.poster-html :deep(img) { 
  width: 100%; 
  height: 400px; 
  object-fit: cover; 
  display: block;
}

.poster-placeholder { 
  height: 100%; 
  display: flex; 
  align-items: center; 
  justify-content: center; 
  color: #94a3b8; 
  font-size: 0.9rem;
  font-weight: 600;
}

/* Meta Styling */
.movie-meta { padding: 1.5rem; }

.movie-title { 
  font-size: 1.25rem; 
  font-weight: 700; 
  color: #1e293b; 
  margin-bottom: 0.25rem; 
}

.movie-year { 
  display: inline-block; 
  font-size: 0.85rem; 
  font-weight: 600; 
  color: #3498db; 
  background: #ebf5fb; 
  padding: 2px 8px; 
  border-radius: 4px; 
  margin-bottom: 1rem;
}

.movie-synopsis { 
  color: #475569; 
  font-size: 0.9rem; 
  line-height: 1.6; 
  display: -webkit-box;
  -webkit-line-clamp: 4;
  -webkit-box-orient: vertical;  
  overflow: hidden;
}

/* Loading Spinner */
.status-msg { text-align: center; padding: 5rem; color: #64748b; }
.spinner { 
  border: 4px solid #f1f5f9; 
  border-top: 4px solid #3498db; 
  border-radius: 50%; 
  width: 50px; 
  height: 50px; 
  animation: spin 1s linear infinite; 
  margin: 0 auto 1.5rem; 
}

@keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

.status-bar.error { 
  background: #fed7d7; 
  color: #822727; 
  padding: 1rem; 
  border-radius: 10px; 
  text-align: center; 
}
</style>
```

## AddMovie.vue

Add a file called `AddMovie.vue` and use the following code:

```html
<script setup>
// --- Configuration ---
const auth = btoa('username:application_password'); 
const baseUrl = 'https://your-site.com/wp-json/wp/v2';

import { reactive, ref } from 'vue';

const isSubmitting = ref(false);
const selectedFile = ref(null);
const message = ref('');
const statusClass = ref('');

const movieData = reactive({
  title: '',
  status: 'publish',
  acf: { synopsis: '', year: '', poster: null }
});

const handleFileChange = (e) => { selectedFile.value = e.target.files[0]; };

const uploadPoster = async () => {
  if (!selectedFile.value) return null;
  const formData = new FormData();
  formData.append('file', selectedFile.value);
  const res = await fetch(`${baseUrl}/media`, {
    method: 'POST',
    headers: { 'Authorization': `Basic ${auth}` },
    body: formData
  });
  const media = await res.json();
  return media.id;
};

const handleFormSubmit = async () => {
  isSubmitting.value = true;
  message.value = 'Uploading movie data...';
  try {
    const posterId = await uploadPoster();
    if (posterId) movieData.acf.poster = posterId;
    const res = await fetch(`${baseUrl}/movies`, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json', 'Authorization': `Basic ${auth}` },
      body: JSON.stringify(movieData)
    });
    if (res.ok) {
      message.value = "Movie added successfully!";
      statusClass.value = "success";
      movieData.title = ''; movieData.acf.synopsis = ''; movieData.acf.year = '';
    }
  } catch (err) {
    message.value = "Failed to connect to WordPress.";
    statusClass.value = "error";
  } finally {
    isSubmitting.value = false;
  }
};
</script>

<template>
  <div class="component-container">
    <h2 class="main-title">Add New Movie</h2>
    <form @submit.prevent="handleFormSubmit" class="wp-form">
      <section class="form-group">
        <label>Movie Title</label>
        <input v-model="movieData.title" type="text" placeholder="Inception" required />
      </section>
      <section class="form-group">
        <label>Synopsis</label>
        <textarea v-model="movieData.acf.synopsis" placeholder="Movie plot..."></textarea>
      </section>
      <section class="form-group">
        <label>Release Year</label>
        <input v-model="movieData.acf.year" type="number" placeholder="2010" />
      </section>
      <section class="form-group">
        <label>Movie Poster</label>
        <input type="file" @change="handleFileChange" accept="image/*" />
      </section>
      <button type="submit" class="primary-btn" :disabled="isSubmitting">
        {{ isSubmitting ? 'Processing...' : 'Add Movie' }}
      </button>
    </form>
    <div v-if="message" :class="['status-bar', statusClass]">{{ message }}</div>
  </div>
</template>

<style scoped>
.component-container { max-width: 650px; margin: 3rem auto; padding: 2.5rem; background: #fff; border-radius: 16px; border: 1px solid #e1e8ed; box-shadow: 0 10px 25px rgba(0,0,0,0.05); font-family: 'Inter', sans-serif; }
.main-title { font-size: 1.75rem; font-weight: 800; color: #1a202c; margin-bottom: 2rem; border-bottom: 2px solid #edf2f7; padding-bottom: 1rem; }
.wp-form { display: flex; flex-direction: column; gap: 1.5rem; }
.form-group { display: flex; flex-direction: column; gap: 0.5rem; }
label { font-size: 0.8rem; font-weight: 700; text-transform: uppercase; color: #4a5568; letter-spacing: 0.05em; }
input, textarea { padding: 12px 16px; border: 2px solid #edf2f7; border-radius: 10px; background: #f8fafc; font-size: 1rem; transition: all 0.2s; }
input:focus, textarea:focus { outline: none; border-color: #3498db; background: #fff; }
.primary-btn { padding: 16px; background: #3498db; color: #fff; font-weight: 700; border: none; border-radius: 10px; cursor: pointer; transition: background 0.2s; }
.primary-btn:disabled { background: #cbd5e0; }
.status-bar { margin-top: 1.5rem; padding: 1rem; border-radius: 10px; text-align: center; font-weight: 600; }
.success { background: #c6f6d5; color: #22543d; }
.error { background: #fed7d7; color: #822727; }
</style>
```

## EditMovie.vue

Add a file called `EditMovie.vue` and use the following code:

```html
<script setup>
// --- Configuration ---
const auth = btoa('username:application_password'); 
const baseUrl = 'https://your-site.com/wp-json/wp/v2';

import { ref, reactive, onMounted } from 'vue';

const movieList = ref([]);
const fetchingList = ref(true);
const selectedId = ref(null);
const isUpdating = ref(false);
const showSuccessModal = ref(false);

const movieData = reactive({
  title: '',
  acf: { synopsis: '', year: '', poster: null }
});

const fetchMovieList = async () => {
  try {
    const res = await fetch(`${baseUrl}/movies?per_page=50`, { headers: { 'Authorization': `Basic ${auth}` } });
    movieList.value = await res.json();
  } finally { fetchingList.value = false; }
};

const selectMovie = (movie) => {
  selectedId.value = movie.id;
  movieData.title = movie.title.rendered;
  movieData.acf.synopsis = movie.acf.synopsis?.simple_value_formatted || '';
  movieData.acf.year = movie.acf.year?.simple_value_formatted || ''; 
  movieData.acf.poster = movie.acf.poster || null;
};

const handleUpdate = async () => {
  isUpdating.value = true;
  try {
    const res = await fetch(`${baseUrl}/movies/${selectedId.value}`, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json', 'Authorization': `Basic ${auth}` },
      body: JSON.stringify({
        title: movieData.title,
        acf: { synopsis: movieData.acf.synopsis, year: movieData.acf.year }
      })
    });
    if (res.ok) { showSuccessModal.value = true; await fetchMovieList(); }
  } finally { isUpdating.value = false; }
};

onMounted(fetchMovieList);
</script>

<template>
  <div class="edit-manager component-container">
    <h2 class="main-title">Manage & Edit Movies</h2>
    
    <ul v-if="!fetchingList" class="movie-grid">
      <li v-for="movie in movieList" :key="movie.id" :class="['movie-card', { active: selectedId === movie.id }]" @click="selectMovie(movie)">
        <div class="card-poster" v-if="movie.acf.poster" v-html="movie.acf.poster.simple_value_formatted"></div>
        <div class="card-content">
          <strong>{{ movie.title.rendered }}</strong>
          <span v-if="movie.acf.year">({{ movie.acf.year.simple_value_formatted }})</span>
        </div>
      </li>
    </ul>

    <section v-if="selectedId" class="edit-form-section">
      <div class="form-header">
        <div v-if="movieData.acf.poster" v-html="movieData.acf.poster.simple_value_formatted" class="form-preview-html"></div>
        <h3>Editing: {{ movieData.title }}</h3>
      </div>
      <form @submit.prevent="handleUpdate" class="wp-form">
        <div class="form-group"><label>Title</label><input v-model="movieData.title" type="text" /></div>
        <div class="form-group"><label>Synopsis</label><textarea v-model="movieData.acf.synopsis"></textarea></div>
        <div class="form-group"><label>Year</label><input v-model="movieData.acf.year" type="number" /></div>
        <div class="form-actions">
          <button type="submit" class="primary-btn" :disabled="isUpdating">Save Update</button>
          <button type="button" @click="selectedId = null" class="secondary-btn">Close</button>
        </div>
      </form>
    </section>

    <div v-if="showSuccessModal" class="modal-overlay">
      <div class="modal">
        <h3>✓ Success</h3>
        <p>Movie updated on WordPress.</p>
        <button @click="showSuccessModal = false" class="primary-btn">Dismiss</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.component-container { max-width: 1100px; margin: 3rem auto; padding: 2.5rem; background: #fff; border-radius: 16px; border: 1px solid #e1e8ed; font-family: 'Inter', sans-serif; }
.main-title { font-size: 1.75rem; font-weight: 800; color: #1a202c; margin-bottom: 2rem; border-bottom: 2px solid #edf2f7; padding-bottom: 1rem; }
.movie-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 1.5rem; list-style: none; padding: 0; margin-bottom: 3rem; }
.movie-card { border: 1px solid #e1e8ed; border-radius: 12px; overflow: hidden; cursor: pointer; transition: 0.3s ease; }
.movie-card.active { border-color: #3498db; background: #f0f7ff; box-shadow: 0 0 0 2px #3498db; }
.card-poster :deep(img) { width: 100%; height: 140px; object-fit: cover; }
.card-content { padding: 12px; font-size: 0.9rem; }
.edit-form-section { background: #f8fafc; padding: 2rem; border-radius: 12px; border: 1px solid #e1e8ed; }
.form-header { display: flex; align-items: center; gap: 1.5rem; margin-bottom: 2rem; }
.form-preview-html :deep(img) { width: 70px; height: 100px; object-fit: cover; border-radius: 6px; }
.wp-form { display: flex; flex-direction: column; gap: 1.5rem; }
.form-group { display: flex; flex-direction: column; gap: 0.5rem; }
label { font-size: 0.8rem; font-weight: 700; text-transform: uppercase; color: #4a5568; }
input, textarea { padding: 12px; border: 2px solid #edf2f7; border-radius: 8px; background: #fff; }
.form-actions { display: flex; gap: 1rem; }
.primary-btn { flex: 1; padding: 14px; background: #3498db; color: #fff; border: none; border-radius: 10px; cursor: pointer; font-weight: 600; }
.secondary-btn { flex: 1; padding: 14px; background: #edf2f7; color: #4a5568; border: none; border-radius: 10px; cursor: pointer; font-weight: 600; }
.modal-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.7); display: flex; align-items: center; justify-content: center; z-index: 1000; }
.modal { background: #fff; padding: 2.5rem; border-radius: 16px; text-align: center; width: 320px; }
</style>
```

## DeleteMovie.vue

Add a file called `DeleteMovie.vue` and use the following code:

```html
<script setup>
// --- Configuration ---
const auth = btoa('username:application_password'); 
const baseUrl = 'https://your-site.com/wp-json/wp/v2';

import { ref, onMounted } from 'vue';

const movieList = ref([]);
const isFetching = ref(true);
const isDeleting = ref(false);
const itemToDelete = ref(null);

const fetchMovies = async () => {
  try {
    const res = await fetch(`${baseUrl}/movies?per_page=50`, { headers: { 'Authorization': `Basic ${auth}` } });
    movieList.value = await res.json();
  } finally { isFetching.value = false; }
};

const confirmDeletion = async () => {
  if (!itemToDelete.value) return;
  isDeleting.value = true;
  try {
    const res = await fetch(`${baseUrl}/movies/${itemToDelete.value.id}`, {
      method: 'DELETE',
      headers: { 'Authorization': `Basic ${auth}` }
    });
    if (res.ok) {
      movieList.value = movieList.value.filter(m => m.id !== itemToDelete.value.id);
      itemToDelete.value = null;
    }
  } finally { isDeleting.value = false; }
};

onMounted(fetchMovies);
</script>

<template>
  <div class="component-container">
    <h2 class="main-title">Movie Inventory</h2>
    <div v-if="isFetching" class="status-msg">Syncing Library...</div>
    <div v-else class="delete-grid">
      <div v-for="movie in movieList" :key="movie.id" class="delete-card">
        <div class="movie-info">
          <strong>{{ movie.title.rendered }}</strong>
          <span v-if="movie.acf.year">{{ movie.acf.year.simple_value_formatted }}</span>
        </div>
        <button @click="itemToDelete = movie" class="danger-btn">Delete</button>
      </div>
    </div>

    <div v-if="itemToDelete" class="modal-overlay">
      <div class="modal">
        <h3>Confirm Deletion</h3>
        <p>Remove <strong>{{ itemToDelete.title.rendered }}</strong>?</p>
        <div class="form-actions">
          <button @click="confirmDeletion" class="danger-btn" :disabled="isDeleting">Yes, Delete</button>
          <button @click="itemToDelete = null" class="secondary-btn">Cancel</button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.component-container { max-width: 900px; margin: 3rem auto; padding: 2.5rem; background: #fff; border-radius: 16px; border: 1px solid #e1e8ed; font-family: 'Inter', sans-serif; }
.main-title { font-size: 1.75rem; font-weight: 800; color: #1a202c; margin-bottom: 2rem; border-bottom: 2px solid #edf2f7; padding-bottom: 1rem; }
.delete-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 1.5rem; }
.delete-card { padding: 1.5rem; border: 1px solid #e2e8f0; border-radius: 12px; display: flex; justify-content: space-between; align-items: center; }
.movie-info { display: flex; flex-direction: column; }
.movie-info strong { color: #1e293b; font-size: 1.05rem; }
.movie-info span { color: #64748b; font-size: 0.85rem; }
.danger-btn { background: #fee2e2; color: #b91c1c; border: none; padding: 8px 16px; border-radius: 8px; font-weight: 600; cursor: pointer; transition: 0.2s; }
.danger-btn:hover { background: #ef4444; color: #fff; }
.secondary-btn { padding: 12px; background: #f1f5f9; color: #475569; border: none; border-radius: 8px; cursor: pointer; flex: 1; }
.modal-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.7); display: flex; align-items: center; justify-content: center; z-index: 1000; }
.modal { background: #fff; padding: 2.5rem; border-radius: 16px; text-align: center; width: 350px; }
.form-actions { display: flex; gap: 1rem; margin-top: 1.5rem; }
.status-msg { text-align: center; color: #64748b; font-style: italic; }
</style>
```
