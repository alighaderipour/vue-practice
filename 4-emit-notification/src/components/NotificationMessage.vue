<script>
export default {
  name: 'NotificationMessage',
  props: {
    message: {
      type: String,
      required: true
    }
  },
  emits: ['dismiss'], // Declaring the event it can emit
  methods: {
    dismissNotification() {
      // Emit an event named 'dismiss'. No payload is needed for this example,
      // as the parent just needs to know the event occurred.
      this.$emit('dismiss');
    }
  }
}
</script>

<template>
  <div>
    <p>{{ message }}</p>
    <button @click="dismissNotification">Dismiss</button>
  </div>
</template>