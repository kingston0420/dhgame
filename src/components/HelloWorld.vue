<template>
  <div class="start" v-if = "!name">
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
    <button @click="restart()" v-else>Restart</button>
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
      bklist: [
      {id:1, name:'Drink', discription:'Take a shot'}, 
      {id:2, name:'Lover', discription:'$name and $name each take a shot'}, 
      {id:3, name:'Master', discription:'Everyone must call you master until the turn is back to you. Slip up = 1 drink.'}, 
      {id:4, name:'Hotseat', discription:'Everyone gets to ask you 3 questions altogether (not each). You must answer honestly, or drink 2 to skip'}, 
      {id:5, name:'Hotseat', discription:'Everyone gets to ask you 3 questions altogether (not each). You must answer honestly, or drink 2 to skip'}, 
      {id:6, name:'Truth or drink', discription:'Name the top three most attractive people in DH or drink 2'}, 
      {id:7, name:'Truth or drink', discription:'Name the top three most attractive people in DH or drink 2'}, 
      {id:8, name:'Name the top three', discription:'Most savage OG execs.'}, 
      {id:9, name:'Name the top three', discription:'Most savage current execs.'}, 
      {id:10, name:'Name the person...', discription:'That has disappointed you the most. Give them a drink.'}, 
      {id:11, name:'Mates', discription:'Pick a buddy! They drink every time you do. Ends after it is your turn again.'}, 
      {id:12, name:'Soju vortex', discription:'JK finish whatever\'s in your glass.'}, 
      {id:13, name:'Stand', discription:'$name Stand up'}],
      list: [
      {id:1, name:'Drink', discription:'Take a shot'}, 
      {id:2, name:'Lover', discription:'$name and $name each take a shot'}, 
      {id:3, name:'Master', discription:'Everyone must call you master until the turn is back to you. Slip up = 1 drink.'}, 
      {id:4, name:'Hotseat', discription:'Everyone gets to ask you 3 questions altogether (not each). You must answer honestly, or drink 2 to skip'}, 
      {id:5, name:'Hotseat', discription:'Everyone gets to ask you 3 questions altogether (not each). You must answer honestly, or drink 2 to skip'}, 
      {id:6, name:'Truth or drink', discription:'Name the top three most attractive people in DH or drink 2'}, 
      {id:7, name:'Truth or drink', discription:'Name the top three most attractive people in DH or drink 2'}, 
      {id:8, name:'Name the top three', discription:'Most savage OG execs.'}, 
      {id:9, name:'Name the top three', discription:'Most savage current execs.'}, 
      {id:10, name:'Name the person...', discription:'That has disappointed you the most. Give them a drink.'}, 
      {id:11, name:'Mates', discription:'Pick a buddy! They drink every time you do. Ends after it is your turn again.'}, 
      {id:12, name:'Soju vortex', discription:'JK finish whatever\'s in your glass.'}, 
      {id:13, name:'Stand', discription:'$name Stand up'}],

      item: {name: 'Welcome to the ultimate DH Game!!!', discription: 'Have your drink ready'}
    }
  },
  methods: {
    submit() {
      this.name = this.i
    },
    restart () {
      this.list = this.bklist.slice();
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
h1 {
  margin: 5px auto;
}
p {
  margin: 20px 50px;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  font-size: 1.5em;
  color:saddlebrown
}
a {
  color: #42b983;
}
.start {
  margin: 10px;
}
.card {
  width: 45vw;
  height: 50vh;
  margin: 0 auto;
  border: 2px solid black;
  border-radius: 20px;
  background-color: cyan;
}
button {
  font-size: 20px;
  margin-top: 1em;
  border-radius: 50px;
  background-color: blueviolet;
  color: white;
  padding: 1em;
}
</style>
