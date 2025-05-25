<script setup>
import { ref } from 'vue';
import BaseModal from './components/BaseModal.vue'; // Adjust path if needed

const isModalOneVisible = ref(false);
const isModalTwoVisible = ref(false);
const isModalThreeVisible = ref(false);
const userName = ref('');
const termsAccepted = ref(false);

const openModalOne = () => isModalOneVisible.value = true;
const closeModalOne = () => isModalOneVisible.value = false;

const openModalTwo = () => isModalTwoVisible.value = true;
const closeModalTwo = () => isModalTwoVisible.value = false;

const openModalThree = () => isModalThreeVisible.value = true;
const closeModalThree = () => isModalThreeVisible.value = false;

const handleConfirmAction = () => {
  alert('Confirmed action from Modal One!');
  closeModalOne();
};

const saveUserName = () => {
  if (userName.value.trim()) {
    alert('User name saved: ' + userName.value);
    closeModalTwo();
    userName.value = ''; // Reset
  } else {
    alert('Please enter a name.');
  }
};

const acceptTerms = () => {
  if (termsAccepted.value) {
    alert('Terms accepted!');
    closeModalThree();
  } else {
    alert('You must accept the terms to proceed.');
  }
};
</script>

<template>
  <div id="app-container">
    <h1>Enhanced Modal Examples 🚀</h1>
    <button @click="openModalOne">Open Informational Modal (Header Slot)</button>
    <button @click="openModalTwo">Open Form Modal (Title Prop)</button>
    <button @click="openModalThree">Open Terms Modal (No Header/Title)</button>

    <BaseModal
      :is-open="isModalOneVisible"
      @close="closeModalOne"
      labelled-by="modal1-title"
      described-by="modal1-desc"
    >
      <template #header>
        <h2 id="modal1-title">Important Information</h2>
      </template>

      <p id="modal1-desc">This modal demonstrates using the header slot for a custom title. It also includes accessibility enhancements like Escape key closing and ARIA attributes. The content behind is not scrollable when this modal is open.</p>
      <p>Try pressing the 'Escape' key to close it.</p>

      <template #footer>
        <button @click="handleConfirmAction" class="button-primary">Confirm</button>
        <button @click="closeModalOne" class="button-secondary">Close</button>
      </template>
    </BaseModal>

    <BaseModal
      :is-open="isModalTwoVisible"
      @close="closeModalTwo"
      title="Enter Your Details"
      labelled-by="modal2-title-prop" described-by="modal2-desc"
    >
      <div id="modal2-desc">
        <label for="userNameInput">Name: </label>
        <input type="text" id="userNameInput" v-model="userName" placeholder="E.g., Alex Smith" />
      </div>
      <p v-if="userName" style="margin-top: 10px;">Preview: Hello, {{ userName }}!</p>

      <template #footer>
        <button @click="saveUserName" class="button-primary">Save</button>
        <button @click="closeModalTwo" class="button-secondary">Cancel</button>
      </template>
    </BaseModal>

     <BaseModal
      :is-open="isModalThreeVisible"
      @close="closeModalThree"
      described-by="modal3-desc"
    >
      <div id="modal3-desc">
        <h3>Terms and Conditions</h3>
        <p style="max-height: 150px; overflow-y: auto; border: 1px solid #eee; padding: 10px; margin-top:5px; margin-bottom:10px;">
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer nec odio. Praesent libero.
            Sed cursus ante dapibus diam. Sed nisi. Nulla quis sem at nibh elementum imperdiet. Duis sagittis ipsum.
            Praesent mauris. Fusce nec tellus sed augue semper porta. Mauris massa. Vestibulum lacinia arcu eget nulla.
            Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos.
        </p>
        <label>
            <input type="checkbox" v-model="termsAccepted" />
            I accept the terms and conditions.
        </label>
      </div>

      <template #footer>
        <button @click="acceptTerms" class="button-primary" :disabled="!termsAccepted">Accept & Proceed</button>
        <button @click="closeModalThree" class="button-secondary">Decline</button>
      </template>
    </BaseModal>
  </div>
</template>

<style>
/* Global styles from your previous example */
#app-container {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  padding: 20px;
  text-align: center; /* Center buttons */
}
h1 {
    margin-bottom: 30px;
}
button {
  padding: 10px 15px;
  margin: 5px; /* Adjusted for better spacing */
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
.button-primary {
  background-color: #007bff;
  color: white;
}
.button-primary:hover {
  background-color: #0056b3;
}
.button-primary:disabled {
  background-color: #a0cfff;
  cursor: not-allowed;
}
.button-secondary {
  background-color: #6c757d;
  color: white;
}
.button-secondary:hover {
  background-color: #545b62;
}
input[type="text"], input[type="checkbox"] {
  padding: 8px;
  margin-top: 5px;
  margin-bottom: 10px; /* Added for spacing */
  border: 1px solid #ccc;
  border-radius: 4px;
}
input[type="text"] {
   width: calc(100% - 22px); /* Full width minus padding & border */
}
label {
  font-weight: bold;
  display: block; /* Make labels block for better layout */
  margin-bottom: 5px;
  text-align: left;
}
/* Specific label styling for checkbox alignment */
label input[type="checkbox"] {
    margin-right: 8px;
    vertical-align: middle;
}
</style>