<script>
export default {
  name: 'BaseModal',
  props: {
    isOpen: {
      type: Boolean,
      default: false
    }
  },
  emits: ['close'], // Declares the 'close' event
  methods: {
    closeModal() {
      this.$emit('close');
    },
    handleOverlayClick(event) {
      // Close modal only if the overlay itself is clicked, not content inside
      if (event.target === this.$refs.modalOverlay) {
        this.closeModal();
      }
    }
  }
}
</script>

<template>
  <div
    v-if="isOpen"
    class="modal-overlay"
    @mousedown="handleOverlayClick"
    ref="modalOverlay"
  >
    <div class="modal-content">
      <header class="modal-header" v-if="$slots.header">
        <slot name="header"></slot>
        <button @click="closeModal" class="modal-close-button" aria-label="Close modal">&times;</button>
      </header>
      <button
        v-else
        @click="closeModal"
        class="modal-close-button modal-close-button-no-header"
        aria-label="Close modal"
      >&times;</button>


      <main class="modal-body">
        <slot>
          <p>This is the default modal content if nothing is provided.</p>
        </slot>
      </main>

      <footer class="modal-footer" v-if="$slots.footer">
        <slot name="footer"></slot>
      </footer>
    </div>
  </div>
</template>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.6);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000; /* Ensure it's on top */
}

.modal-content {
  background-color: white;
  padding: 25px;
  border-radius: 8px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
  min-width: 300px;
  max-width: 90%;
  max-height: 90vh; /* Max height */
  overflow-y: auto; /* Scroll if content overflows */
  position: relative; /* For positioning the close button */
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #eee;
  padding-bottom: 15px;
  margin-bottom: 15px;
  font-size: 1.25em;
}

.modal-close-button {
  background: none;
  border: none;
  font-size: 1.8em;
  line-height: 1;
  cursor: pointer;
  padding: 0 5px;
  color: #888;
}
.modal-close-button:hover {
  color: #333;
}
.modal-close-button-no-header {
  position: absolute;
  top: 10px;
  right: 10px;
  font-size: 1.5em; /* Slightly smaller if no header */
}


.modal-body {
  margin-bottom: 20px;
  line-height: 1.6;
}

.modal-footer {
  border-top: 1px solid #eee;
  padding-top: 15px;
  margin-top: 15px;
  display: flex;
  justify-content: flex-end; /* Align buttons to the right by default */
  gap: 10px; /* Space between footer items */
}

/* Basic button styling for footer examples */
:slotted(footer button) { /* Example of styling slotted content, use with caution or pass classes */
  padding: 8px 15px;
  border-radius: 4px;
  cursor: pointer;
}
</style>
