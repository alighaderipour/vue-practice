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