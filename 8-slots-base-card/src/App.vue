<script>
import BaseCard from "./components/BaseCard.vue";

export default {
  name: "App",
  components: {
    BaseCard,
  },
  data() {
    return {
      article: {
        title: "Understanding Vue Slots",
        content:
          "Slots are a powerful feature in Vue.js for creating flexible and reusable components. They allow you to pass template fragments from a parent component into designated areas within a child component.",
        author: "AI Assistant",
        date: "May 24, 2025",
      },
      eventInfo: {
        name: "Vue Conference 2025",
        details:
          "Join us for the biggest Vue event of the year! Learn from experts, network with peers, and explore the future of Vue.js.",
        location: "Virtual",
      },
    };
  },
};
</script>

<template>
  <div id="app-container">
    <h1>My Content Hub</h1>

    <BaseCard>
      <template v-slot:header>
        <h2>{{ article.title }}</h2>
      </template>

      <p>{{ article.content }}</p>
      <button @click="alert('Read more about ' + article.title)">
        Read More
      </button>

      <template #footer>
        <span>By {{ article.author }} on {{ article.date }}</span>
      </template>
    </BaseCard>

    <BaseCard>
      <template #header>
        <h3>Event: {{ eventInfo.name }}</h3>
      </template>

      <p>{{ eventInfo.details }}</p>
      <p><strong>Location:</strong> {{ eventInfo.location }}</p>
    </BaseCard>

    <BaseCard>
      <template #header>
        <h4>Quick Reminder</h4>
      </template>
    </BaseCard>

    <BaseCard>
      <p>
        This card only has custom body content. No header, no footer from the
        parent.
      </p>
      <p>The <code>BaseCard</code> component's default slot makes this easy.</p>
    </BaseCard>
  </div>
</template>

<style>
/* Global styles for the app container if needed */
#app-container {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  padding: 20px;
  background-color: #f4f7f6;
}

h1 {
  text-align: center;
  margin-bottom: 30px;
}
</style>
