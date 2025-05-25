<script>
export default {
  name: 'FeedbackInput',
  data() {
    return {
      feedbackText: '' // To store the text from the input field
    }
  },
  emits: ['feedback-submitted'], // Good practice to declare emitted events
  methods: {
    submitFeedback() {
      if (this.feedbackText.trim() === '') {
        alert('Please enter some feedback before submitting.');
        return;
      }
      // Emit an event named 'feedback-submitted' with the feedbackText as the payload
      this.$emit('feedback-submitted', this.feedbackText);
      this.feedbackText = ''; // Clear the input field after submitting
    }
  }
}
</script>

<template>
  <div class="feedback-input-container">
    <input
      type="text"
      v-model="feedbackText"
      placeholder="Enter your feedback here..."
    />
    <button @click="submitFeedback">Send Feedback</button>
  </div>
</template>

<style scoped>
.feedback-input-container {
  border: 1px solid #ccc;
  padding: 15px;
  margin-bottom: 20px;
  border-radius: 5px;
}
input[type="text"] {
  margin-right: 10px;
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 3px;
}
button {
  padding: 8px 15px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 3px;
  cursor: pointer;
}
button:hover {
  background-color: #0056b3;
}
</style>