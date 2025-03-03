<script>
export default {
  data() {
    return {
      message: 'Hello, Vue.js!',
      status: 'unknown', // Changed to 'unknown' to see if the button changes it
      tasks: ['Task One', 'Task Two', 'Task Three', 'Task Four'],
      link: 'http://www.google.com',
    };
  },
  methods: {
    setSuccess() { // ✅ Explicit method to update status
      this.status = 'success';
    }
  }
};
</script>

<template>
  <h1>{{ message }}</h1>
  <p v-if="status === 'success'">The status is success.</p>
  <p v-else-if="status === 'error'">The status is error.</p>
  <p v-else>The status is unknown.</p>

  <h3>Tasks</h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>
  <!--<a v-bind:href="link" target="_blank">Visit Google</a>-->
  <a :href="link" target="_blank">Visit Google</a>

  <br />
  <!-- <button v-on:click="setSuccess">Set Success</button> -->
  <button @click="setSuccess">Set Success</button>
</template>
