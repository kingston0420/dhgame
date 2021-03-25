<template>
  <div class="start" v-if = "!name">
    Enter your name
    <input type="text" name="" v-model="i" placeholder="Type your name here" />
    <a @click="submit()">Submit!</a>
  </div>
  <div class="card" v-if="list.length > 0">
    <h1>{{ item.name }}</h1>
    <p>{{item.discription}}</p>
  </div>
  <div class="card" v-else>
    <h1>The end</h1>
    <p>Game over</p>
  </div>
  <div class="button">
    <button @click="next()" v-if="list.length > 0">Next Question</button>
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
      i: '',
      name: null,
      list: [{id:1, name:'Drink', discription:'$name Drink a cup'}, {id:2, name:'Sit', discription:'$name Sit down'}, {id:3, name:'Stand', discription:'$name Stand up'}], 
      item: {name: 'Welcome', discription: 'Hello world'}
    }
  },
  methods: {
    submit() {
      this.name = this.i
    },
    next() {
      this.item = this.list[Math.floor(Math.random()*this.list.length)]
      this.item.discription = this.item.discription.replace('$name', this.name)
      var i = this.item
      this.list = this.list.filter(function(o){
        return o.id != i.id
      })
    }
  },
  mounted() {

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
.card {
  width: 50vw;
  height: 50vh;
  margin: 0 auto;
  border: 1px solid black;
  border-radius: 50px;
}
button {
  font-size: 22px;
  margin-top: 2em;
  border-radius: 50px;
  background-color: blueviolet;
  color: white;
  padding: 1em;
}
</style>
