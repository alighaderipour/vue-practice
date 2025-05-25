<script>
import User from './components/User.vue'

export default {
  name: 'App',
  components: {
    User
  },
  data() {
    return {
      receivedFeedback: 'No feedback yet.' // To store and display the feedback
    }
  },
  methods: {
    handleNewFeedback(feedbackPayload) {
      // This method is called when the 'feedback-submitted' event is received
      // The 'feedbackPayload' will be the text emitted from User.vue
      this.receivedFeedback = feedbackPayload;
    }
  }
}
</script>

<template>
  <div id="app-container">
    <h1>Feedback Area</h1>
    <User @feedback-submitted="handleNewFeedback" />
    <div class="feedback-display">
      <h2>Latest Feedback Received:</h2>
      <p>{{ receivedFeedback }}</p>
    </div>
  </div>
</template>

<style>
#app-container {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.feedback-display {
  margin-top: 20px;
  padding: 15px;
  border: 1px solid #e0e0e0;
  background-color: #f9f9f9;
  border-radius: 5px;
}
.feedback-display h2 {
  margin-top: 0;
}
</style>