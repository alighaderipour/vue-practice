<script setup>
import { defineProps, defineEmits, onMounted, onUnmounted, watch, ref } from 'vue';

const props = defineProps({
  isOpen: {
    type: Boolean,
    default: false
  },
  // Optional: A title prop if you don't want to use the header slot for simple titles
  title: {
    type: String,
    default: ''
  },
  // Optional: An ID for the element that labels the modal (for aria-labelledby)
  labelledBy: {
    type: String,
    default: null
  },
  // Optional: An ID for the element that describes the modal (for aria-describedby)
  describedBy: {
    type: String,
    default: null
  }
});

const emit = defineEmits(['close']);

const modalOverlay = ref(null);
const modalContent = ref(null); // Ref for the modal content div

const closeModal = () => {
  emit('close');
};

const handleOverlayClick = (event) => {
  if (event.target === modalOverlay.value) {
    closeModal();
  }
};

const handleEscapeKey = (event) => {
  if (event.key === 'Escape' && props.isOpen) {
    closeModal();
  }
};

watch(() => props.isOpen, (newVal) => {
  if (newVal) {
    document.body.style.overflow = 'hidden'; // Prevent background scrolling
    // Focus management: Focus the modal content or first interactive element
    // For a more robust solution, a full focus trap is needed.
    // This is a basic example:
    requestAnimationFrame(() => { // Wait for next tick after modal is rendered
      if (modalContent.value) {
        modalContent.value.focus(); // Focus the modal content div itself
      }
    });
  } else {
    document.body.style.overflow = '';
  }
});

onMounted(() => {
  document.addEventListener('keydown', handleEscapeKey);
});

onUnmounted(() => {
  document.removeEventListener('keydown', handleEscapeKey);
  document.body.style.overflow = ''; // Ensure overflow is reset if component is destroyed while open
});
</script>

<template>
  <Teleport to="body">
    <Transition name="modal-fade">
      <div
        v-if="isOpen"
        class="modal-overlay"
        @mousedown="handleOverlayClick"
        ref="modalOverlay"
      >
        <div
          class="modal-content"
          ref="modalContent"
          role="dialog"
          aria-modal="true"
          :aria-labelledby="labelledBy || ($slots.header ? 'modal-header-slot' : 'modal-title-prop')"
          :aria-describedby="describedBy || 'modal-body-slot'"
          tabindex="-1" >
          <header class="modal-header" v-if="$slots.header || title">
            <slot name="header">
              <h2 v-if="title" :id="labelledBy || 'modal-title-prop'">{{ title }}</h2>
            </slot>
            <button @click="closeModal" class="modal-close-button" aria-label="Close modal">&times;</button>
          </header>
          <button
            v-else
            @click="closeModal"
            class="modal-close-button modal-close-button-no-header"
            aria-label="Close modal"
          >&times;</button>

          <main class="modal-body" :id="describedBy || 'modal-body-slot'">
            <slot>
              <p>This is the default modal content if nothing is provided.</p>
            </slot>
          </main>

          <footer class="modal-footer" v-if="$slots.footer">
            <slot name="footer"></slot>
          </footer>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

<style scoped>
.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity 0.3s ease;
}
.modal-fade-enter-from,
.modal-fade-leave-to {
  opacity: 0;
}

/* ... (keep all your existing modal styles from the previous example) ... */
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
  z-index: 1000;
}

.modal-content {
  background-color: white;
  padding: 25px;
  border-radius: 8px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
  min-width: 300px;
  max-width: 90%;
  max-height: 90vh;
  overflow-y: auto;
  position: relative;
}
.modal-content:focus { /* Style for when modal content is focused */
  outline: 2px solid var(--primary-color, #007bff); /* Or your preferred focus style */
  outline-offset: 2px;
}


.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #eee;
  padding-bottom: 15px;
  margin-bottom: 15px;
}
.modal-header h2 { /* Added for default title styling */
    font-size: 1.25em;
    margin: 0;
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
  font-size: 1.5em;
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
  justify-content: flex-end;
  gap: 10px;
}

/* :slotted selector has limitations and might not be ideal for complex styling.
   It's often better to pass classes to slotted content from the parent.
   Keep it if it works for your simple button case. */
:slotted(footer button) {
  padding: 8px 15px;
  border-radius: 4px;
  cursor: pointer;
}
</style>