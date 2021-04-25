<template>
  <div class="home">
    <img alt="DH logo" src="../assets/blue_white.png">
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
    margin-top: 10px;
    width: 70px
  }
  .home {
    background-color: #073464;
    height: 100vh;
  }
</style>
