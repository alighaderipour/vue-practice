<script>
export default {
  name: 'BaseCard',
}
</script>

<template>
  <div class="card">
    <header class="card-header" v-if="$slots.header">
      <slot name="header"></slot>
    </header>

    <main class="card-body">
      <slot>
        <p>This is the default card content if nothing else is provided.</p>
      </slot>
    </main>

    <footer class="card-footer" v-if="$slots.footer">
      <slot name="footer"></slot>
    </footer>
  </div>
</template>

<style scoped>
.card {
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  margin: 15px;
  padding: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  background-color: #ffffff;
  overflow: hidden; /* Ensures padding and borders are respected by children */
}

.card-header {
  border-bottom: 1px solid #eeeeee;
  padding-bottom: 15px;
  margin-bottom: 15px;
  font-size: 1.25em;
  font-weight: bold;
  color: #333;
}

.card-body {
  color: #555;
  line-height: 1.6;
}

.card-footer {
  border-top: 1px solid #eeeeee;
  padding-top: 15px;
  margin-top: 15px;
  font-size: 0.9em;
  color: #777;
}
</style>
