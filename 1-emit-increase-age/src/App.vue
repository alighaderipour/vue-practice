<script>
import User from './components/User.vue'
export default {
    name: 'App',
    data() {
        return {
          age:20
        }
    },
    methods:{
      increaseAge(num){
        this.age +=num
      }
    },
    components:{
      User
    }
}
</script>

<template>
    <div>
      <User :age="age" @increase-age="increaseAge"></User>
    </div>
</template>

<style>
</style>