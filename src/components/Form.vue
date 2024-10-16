<template>
  <div>
    <form @submit.prevent="sendData">
      <input v-model="username" placeholder="Enter your name" />
      <button type="submit">Send</button>
    </form>
    <p v-if="responseMessage">{{ responseMessage }}</p>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      username: '',
      responseMessage: ''
    };
  },
  methods: {
    async sendData() {
      try {
        const response = await axios.post('http://localhost:5000/api/users', {
          name: this.username
        });
        this.responseMessage = 'User added successfully!';
      } catch (error) {
        console.error('There was an error:', error);
        this.responseMessage = 'Failed to add user.';
      }
    }
  }
};
</script>

