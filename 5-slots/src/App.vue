<script>
// Corrected import name to 'Form'
import Form from './components/Form.vue'; // Ensure path is correct

export default {
  name: 'App', // It's good practice to name your components
  data() {
    return {
      randomName: "this is sparta"
    }
  },
  components: {
    Form // Registering the Form component
  }
}
</script>

<template>
  <div>
    <h1>My Application</h1>
    <Form>
      <p>This content is from App.vue:</p>
      <h2>{{ randomName }}</h2>
      <button>A button from App.vue!</button>
      </Form>

    <Form>
      <p>Another instance of the Form component with different content.</p>
      <em>Pretty flexible!</em>
    </Form>
  </div>
</template>

<style>
/* Global styles or App.vue specific styles */
h1 {
  color: #333;
}
</style>