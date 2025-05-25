<script>
import InputForm from "./components/InputForm.vue";
export default {
  name: "App",
  data() {
    return {
      textFeedback: "",
    };
  },
  components: {
    InputForm,
  },
  methods: {
    getFeedback(text) {
      this.textFeedback = "";
      this.textFeedback = text;
    },
  },
};
</script>

<template>
  <div>
    <inputForm @share-feedback="getFeedback" />
    <p>{{ textFeedback }}</p>
  </div>
</template>

<style></style>
