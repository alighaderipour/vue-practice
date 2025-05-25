<script>
import BaseCard from "./components/BaseCard.vue"; // Adjust path if necessary

export default {
  name: "App",
  components: {
    BaseCard,
  },
  data() {
    return {
      currentUser: {
        name: "Jane Doe",
        title: "Lead Developer",
        status: "Online",
      },
      latestArticle: {
        title: "Vue 3 Slots Explained",
        excerpt: "A deep dive into the new slot syntax and features...",
        author: "A. N. Other",
      },
      quickNoteContent: "Remember to buy groceries after work!",
    };
  },
  methods: {
    handleButtonClick(message) {
      alert(message);
    },
  },
};
</script>

<template>
  <div id="app-container">
    <h1>My Application Using BaseCard</h1>

    <BaseCard>
      <template #header>
        <div class="app-card-header">
          <h2>User Profile: {{ currentUser.name }}</h2>
          <p><em>{{ currentUser.title }}</em></p>
        </div>
      </template>

      <div class="app-card-body">
        <p>Status: {{ currentUser.status }}</p>
        <p>This content is placed in the default slot from App.vue.</p>
      </div>

      <template v-slot:footer>
        <div class="app-card-footer">
          <button @click="handleButtonClick('Editing profile for ' + currentUser.name)">Edit Profile</button>
        </div>
      </template>
    </BaseCard>

    <BaseCard>
      <template #header>
        <div class="app-card-header">
          <h3>Latest Article</h3>
        </div>
      </template>

      <div class="app-card-body">
        <h4>{{ latestArticle.title }}</h4>
        <p>{{ latestArticle.excerpt }}</p>
        <small>By: {{ latestArticle.author }}</small>
      </div>
    </BaseCard>

    <BaseCard>
      <div class="app-card-body">
        <p><strong>Quick Note:</strong></p>
        <p>{{ quickNoteContent }}</p>
        <p><em>This card only has custom body content. The header and footer are not used.</em></p>
      </div>
    </BaseCard>

    <BaseCard>
      <template v-slot:header>
        <div class="app-card-header">
          <h4>System Status</h4>
        </div>
      </template>
    </BaseCard>

    <BaseCard>
    </BaseCard>

  </div>
</template>

<style>
/* Global styles for the App or unscoped styles */
body {
  font-family: sans-serif;
  background-color: #f0f2f5;
  padding: 20px;
  color: #333;
}

#app-container {
  max-width: 900px;
  margin: 0 auto;
}

h1 {
  color: #2c3e50;
  text-align: center;
  margin-bottom: 30px;
}

/* Styles for the BaseCard container itself (Ideally, these would be in BaseCard.vue <style scoped>) */
/* Since BaseCard.vue has no <style> block, we can add some basic styling here for demonstration */
.card-container {
  background-color: #fff;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  margin-bottom: 25px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  padding: 20px; /* Added padding here as BaseCard no longer has internal header/main/footer wrappers with padding */
}

/* Styles for the content App.vue injects into the slots */
.app-card-header {
  border-bottom: 1px solid #eee;
  padding-bottom: 15px;
  margin-bottom: 15px;
}

.app-card-header h2, .app-card-header h3, .app-card-header h4 {
  margin-top: 0;
  color: #1a5f7a;
}

.app-card-header em {
  font-size: 0.9em;
  color: #555;
}

.app-card-body p {
  line-height: 1.6;
}

.app-card-body strong {
  color: #333;
}

.app-card-footer {
  border-top: 1px solid #eee;
  padding-top: 15px;
  margin-top: 15px;
  text-align: right;
}

.app-card-footer button {
  background-color: #007bff;
  color: white;
  border: none;
  padding: 10px 15px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 0.9em;
}

.app-card-footer button:hover {
  background-color: #0056b3;
}
</style>