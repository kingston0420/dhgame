<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>{{item.name}}</p>
    <p>{{item.discription}}</p>
    <button @click="next()">Next Question</button>
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
      list: [{name:'Drink', discription:'Drink a cup'}, {name:'Sit', discription:'Sit down'}, {name:'Stand', discription:'Stand up'}], 
      item: ''
    }
  },
  methods: {
    next() {
      this.item = this.list[Math.floor(Math.random()*this.list.length)]
      this.list = this.list.filter(function(o){
        return o.name != this.item.name
      })
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
