<script>
import NotificationMessage from './components/NotificationMessage.vue'; // Adjust path if needed

export default {
  name: 'App',
  components: {
    NotificationMessage
  },
  data() {
    return {
      showNotification: false,
      notificationText: ''
    }
  },
  methods: {
    triggerNotification() {
      this.notificationText = 'This is an important update! (Emitted from child to parent)';
      this.showNotification = true;
    },
    handleDismiss() {
      // This method is called when the 'dismiss' event is received from the child
      this.showNotification = false;
      this.notificationText = ''; // Optional: clear the text
      console.log('Notification dismissed by parent!');
    }
  }
}
</script>

<template>
  <div>
    <h1>App</h1>
    <button @click="triggerNotification">Show Sample Notification</button>

    <NotificationMessage
      v-if="showNotification"
      :message="notificationText"
      @dismiss="handleDismiss"
    />

    <p v-if="!showNotification">No active notifications.</p>
  </div>
</template>