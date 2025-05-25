<script>
export default {
  name: "InputForm",
  data() {
    return {
      inputText: "",
    };
  },
  methods: {
    shareFeedback() {
      if (!this.inputText.trim()) alert("empty")
      this.$emit("share-feedback", this.inputText);
    this.inputText=""

    },
  },
  emits: ["share-feedback"],
};
</script>

<template>
  <div>
    <input
      type="text"
      placeholder="share your feedback here"
      v-model="inputText"
    />
    <button @click="shareFeedback">submit</button>
  </div>
</template>

<style></style>
