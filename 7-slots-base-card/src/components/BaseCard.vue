<script>
export default {
  name: 'BaseCard',
  // This component doesn't need its own data or methods for this example
  // It's purely a presentational component whose content is driven by slots
}
</script>

<template>
  <div class="card-container">
    <header class="card-header" v-if="$slots.header">
      <slot name="header"></slot>
    </header>

    <main class="card-body">
      <slot>
        <p>This is the default card body.</p>
      </slot>
    </main>

    <footer class="card-footer" v-if="$slots.footer">
      <slot name="footer"></slot>
    </footer>
  </div>
</template>

<style scoped>
.card-container {
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  padding: 16px;
  margin: 20px 0;
  background-color: #fff;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.05);
}

.card-header {
  margin-bottom: 12px;
  border-bottom: 1px solid #ddd;
  padding-bottom: 8px;
  font-weight: bold;
  font-size: 1.2em;
}

.card-body {
  margin-bottom: 12px;
  font-size: 1em;
  color: #333;
}

.card-footer {
  border-top: 1px solid #ddd;
  padding-top: 8px;
  display: flex;
  gap: 10px;
  justify-content: flex-end;
}

button {
  padding: 6px 12px;
  background-color: #007bff;
  border: none;
  color: white;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
</style>