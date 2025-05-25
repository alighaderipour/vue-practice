<script>
import BaseModal from './components/BaseModal.vue';

export default {
  name: 'App',
  components: {
    BaseModal
  },
  data() {
    return {
      isModalOneVisible: false,
      isModalTwoVisible: false,
      userName: ''
    }
  },
  methods: {
    openModalOne() {
      this.isModalOneVisible = true;
    },
    closeModalOne() {
      this.isModalOneVisible = false;
    },
    openModalTwo() {
      this.isModalTwoVisible = true;
    },
    closeModalTwo() {
      this.isModalTwoVisible = false;
    },
    handleConfirmAction() {
      alert('Confirmed action from Modal One!');
      this.closeModalOne();
    },
    saveUserName() {
      if (this.userName.trim()) {
        alert('User name saved: ' + this.userName);
        this.closeModalTwo();
        this.userName = ''; // Reset for next time
      } else {
        alert('Please enter a name.');
      }
    }
  }
}
</script>

<template>
  <div id="app-container">
    <h1>Modal Slot Practice</h1>
    <button @click="openModalOne">Open Informational Modal</button>
    <button @click="openModalTwo" style="margin-left: 10px;">Open Form Modal</button>

    <BaseModal :is-open="isModalOneVisible" @close="closeModalOne">
      <template #header>
        <h2>Important Information</h2>
      </template>

      <p>This is an example of a modal dialog created using Vue slots.</p>
      <p>The header, body, and footer content are all passed in from this parent component (App.vue), making the <code>BaseModal</code> component highly reusable.</p>

      <template #footer>
        <button @click="handleConfirmAction" class="button-primary">Confirm</button>
        <button @click="closeModalOne" class="button-secondary">Close</button>
      </template>
    </BaseModal>

    <BaseModal :is-open="isModalTwoVisible" @close="closeModalTwo">
      <template #header>
        <h3>Enter Your Name</h3>
      </template>

      <div>
        <label for="userNameInput">Name: </label>
        <input type="text" id="userNameInput" v-model="userName" placeholder="E.g., Jane Doe" />
      </div>
      <p v-if="userName">Hello, {{ userName }}!</p>


      <template #footer>
        <button @click="saveUserName" class="button-primary">Save Name</button>
        <button @click="closeModalTwo" class="button-secondary">Cancel</button>
      </template>
    </BaseModal>

  </div>
</template>

<style>
/* Some basic global styles for the App page */
#app-container {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  padding: 20px;
}
button {
  padding: 10px 15px;
  margin-right: 8px;
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
.button-secondary {
  background-color: #6c757d;
  color: white;
}
.button-secondary:hover {
  background-color: #545b62;
}
input[type="text"] {
  padding: 8px;
  margin-top: 5px;
  border: 1px solid #ccc;
  border-radius: 4px;
  width: calc(100% - 18px); /* Full width minus padding */
}
label {
  font-weight: bold;
}
</style>
