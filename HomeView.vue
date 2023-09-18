<template>
  <div>
    <!-- 1. Movie Details -->
    
    <h2>Movie Details</h2>
    <p>Title: {{ movieTitle }}</p> <!-- a. Text Interpolation -->
    <p>Director: {{ director }}</p>
    <p v-html="movieDescription"></p> <!-- b. Raw HTML [v-html] -->

    <!-- 2. Movie Theatre -->
    <p :id="theaterId"></p> <!-- c. Attribute Bindings [v-bind:id] -->

    <!-- 3. Release Date -->
    <p>Release Date: {{ releaseDate }}</p> <!-- d. JavaScript expressions inside syntax -->

    <!-- 4. Movie Actions -->
    <button @click="startMovie">Start Movie</button> <!-- 2. Methods -->

    <!-- 5. Audience Reactions -->
    <h2>Audience Reactions</h2>
    <p>Total Viewers: {{ totalViewers }}</p>
    <p>Total Applauses: {{ totalApplauses }}</p>

    <!-- 6. Cast List -->
    <h2>Cast List</h2>
    <ul>
      <li v-for="actor in cast" :key="actor.id">{{ actor.name }}</li>
    </ul> <!-- a. v-for with an Object -->

    <!-- 7. Event Handling: Movie Events -->
    <button @click="applause"> Applause </button> <!-- a. Inline Handlers -->
    <button @click="viewers">    Viewers </button> <!-- b. Method Handlers -->
    <!-- 8. Movie Reservation Form -->
    <h2>Reserve a Seat</h2>
    <label for="seatNumber">Seat Number:</label>
    <input type="number" v-model="seatNumber" /> <!-- a. v-model with <input type="number"> -->
    <br />
    <label for="ticketType">Ticket Type:</label>
    <select v-model="ticketType">  <!-- a. v-model with <select> -->
      <option value="standard">Standard</option>
      <option value="vip">VIP</option>
    </select> 
    <br />
    <label for="reservationNotes">Reservation Notes:</label>
    <textarea v-model="reservationNotes"></textarea> <!-- a. v-model with <textarea> -->

    <!-- 9. Movie Watchers -->
    
    <div>
    <h2>Movie Watchers</h2>
    <p>Seat Number Watcher: {{ seatNumber }}</p>
    
  </div>

    <!-- 10. Movie Components -->
    
    <movie-summary :summary="movieSummary"></movie-summary>
    <!-- a. Props -->
    <audience-stats @applause="handleApplauseEvent"></audience-stats>
    <slot-example>
        <!-- c. Slots -->
      <!-- Content for the slot -->
    </slot-example>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue';

// 1. Movie Details
const movieTitle = ref('Rocky aur Rani ki Prem Kahani');
const director = ref('Karan Johar');
const movieDescription = '<p>An exciting movie experience!</p>';
const theaterId = 'Village Cinema';
const releaseDate = '2023-09-18';

// 4. Movie Actions
const startMovie = () => {
  alert('The movie has started!');
};

// 5. Audience Reactions
const totalViewers = ref(0);
const totalApplauses = ref(0);

// 6. Cast List
const cast = ref([
  { id: 1, name: 'Ranveer Singh' },
  { id: 2, name: 'Alia Bhatt' },
  { id: 3, name: 'Dharmendra' },
]);

// 7. Event Handling: Movie Events
const applause = () => {
  totalApplauses.value++;
};
const viewers = () => {
  totalViewers.value++;
};

// 8. Movie Reservation Form
const seatNumber = ref(0);
const ticketType = ref('');
const reservationNotes = ref('');

// 9. Movie Watchers
// Define watchers using the watch API
watch(
  () => seatNumber.value,
  (newValue, oldValue) => {
    // Handle changes in seatNumber
    console.log(`Seat number changed from ${oldValue} to ${newValue}`);
    // You can perform additional actions here
  }
);


// 10. Movie Components
const movieSummary = ref('');
const handleApplauseEvent = () => {
  // Handle applause event from audience-stats component
};
</script>
<style scoped>
body {
  background-color: skyblue; 
  margin: 0; 
  padding: 0; 
  font-family: Arial, sans-serif;
}

.movie-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: skyblue;
  border: 1px solid #ccc;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  font-family: Arial, sans-serif;
}

h2 {
  color: #333;
  margin-top: 10px;
}

p {
  margin: 5px 0;
}

button {
  background-color: #007bff;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin-top: 10px;
  cursor: pointer;
  border-radius: 3px;
}

button:hover {
  background-color: #0056b3;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  margin: 5px 0;
}

label {
  display: block;
  margin-top: 10px;
  font-weight: bold;
}

input[type="number"],
select,
textarea {
  width: 100%;
  padding: 5px;
  margin: 5px 0;
  border: 1px solid #ccc;
  border-radius: 3px;
}

.movie-description {
  background-color: skyblue;
  padding: 10px;
  border: 1px solid #ccc;
  margin-top: 10px;
}
</style>