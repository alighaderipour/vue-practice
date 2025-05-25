<script>
export default {
  name: 'Form', // It's good practice to name your components
  data() {
    return {
      // Form-specific data could go here if needed
    }
  }
}
</script>

<template>
  <div>
    <slot></slot>
  </div>
</template>

<style>
/* Styles for the Form component itself */
div {
  border: 1px solid #ccc;
  padding: 20px;
  margin: 10px;
  border-radius: 5px;
  background-color: #f9f9f9;
}
</style>