<script setup>
import { ref, onMounted } from 'vue'; // Import Vue's Composition API functions

// Reactive state variables
const message = ref('Hello, Vue.js!'); // A welcome message
const status = ref('unknown'); // Tracks status ('unknown', 'success', 'error')
const tasks = ref(['Task One', 'Task Two', 'Task Three', 'Task Four']); // Initial task list
const link = ref('http://www.google.com'); // Link to Google
const newTask = ref(''); // Stores user input for a new task

// Function to set status as 'success'
const setSuccess = () => {
  status.value = 'success'; // Updating the reactive status variable
};

// Function to add a new task to the list
const addTask = () => {
  if (newTask.value.trim() === '') {
    return; // Prevent adding empty tasks
  }
  tasks.value.push(newTask.value); // Add new task to the list
  newTask.value = ''; // Clear input field after submission
};

// Function to remove a task by index
const removeTask = (index) => {
  tasks.value.splice(index, 1); // Remove task at the given index
};

// Fetch tasks from an API when the component is mounted
onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos'); // Fetch dummy tasks
    const data = await response.json(); // Convert response to JSON
    tasks.value = data.map((task) => task.title); // Extract and store task titles
  } catch (error) {
    console.log('Error fetching tasks'); // Handle fetch errors
  }
});
</script>

<template>
  <!-- Display welcome message -->
  <h1>{{ message }}</h1>

  <!-- Conditionally render status messages -->
  <p v-if="status === 'success'">The status is success.</p>
  <p v-else-if="status === 'error'">The status is error.</p>
  <p v-else>The status is unknown.</p>

  <!-- Form to add a new task -->
  <form @submit.prevent="addTask">
    <input type="text" id="newTask" name="newTask" v-model="newTask" />
    <label for="newTask">Add Task</label>
    <button type="submit">Submit</button>
  </form>

  <!-- Task list -->
  <h3>Tasks</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="index"> <!-- Use index as key to avoid duplicate issues -->
      <span>{{ task }}</span>
      <button @click="removeTask(index)">Remove</button> <!-- Remove task on button click -->
    </li>
  </ul>

  <!-- External link -->
  <a :href="link" target="_blank">Visit Google</a>

  <br />

  <!-- Button to update status -->
  <button @click="setSuccess">Set Success</button>
</template>
