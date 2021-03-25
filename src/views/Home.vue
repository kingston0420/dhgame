<template>
  <div class="home">
    <img alt="DH logo" src="../assets/DH.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  }
}
</script>

<style scoped>
  img {
    width: 100px
  }
  .home {
  background-color: darkorange;
  }
</style>
