<script>
export default {
    name: 'User',
    data() {
        return {
        }
    },
    emits:[
        "increase-age"
    ],
    methods:{
    changeAge(){
        this.$emit("increase-age",3)
    },
  
},
props:{
      age:{
        type: Number,
        required: true
      }
    }
}
</script>

<template>
  <div>
    <button @click="changeAge">update age</button>
    <p> {{ age }}</p>
  </div>
</template>

<style></style>
