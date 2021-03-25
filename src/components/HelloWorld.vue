<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>{{item}}</p>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      list: ['Drink', 'Sit', 'Stand'], 
      item: ''
    }
  },
  mounted() {
    this.item = this.list[Math.floor(Math.random()*this.list.length)]
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
