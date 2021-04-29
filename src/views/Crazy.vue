<template>
<div class="home">
  <img alt="DH logo" src="../assets/DH.png">
  <div class="start" v-if = "!name">
    <spam>This version is still in the making. Please contribute to the the card and your idea can be a part of this game</spam>
    <br>
    <a href="https://docs.google.com/spreadsheets/d/1XmymgqbUaoW_CC1TnG8Q7YbeA3YsXr03UWrCKNXm79Q/edit#gid=0" target="_blank">Contribute here</a>
    <!--<spam>Player: &nbsp;</spam>-->
    <span class="nameList" v-for="n in nameList" v-bind:key=n>{{n}} &nbsp;&nbsp;</span>
    <br>
    <spam>Enter your name</spam>
    <input type="text" name="" v-model="i" placeholder="Type your name here" />
    <button class="submit" @click="submit()">Submit!</button>
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
    <button class="restartButton" @click="next()" v-if="flag == 1">Start Game</button>
    <button @click="next()" v-else-if="list.length > 0 && flag == 0">Next Card</button>
    <button class="restartButton" @click="restart()" v-else>Restart</button>
  </div>
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
      flag: 1,
      i: '',
      name: null,
      nameList: [],
      bklist: [
      {id:1, name:'Drink', discription:'Take a shot'}, 
      {id:2, name:'Lover', discription:'$name and $name each take a shot'}  
      ],

      list: [
      {id:1, name:'Drink', discription:'Take a shot'}, 
      {id:2, name:'Lover', discription:'$name and $name each take a shot'} 
      ],

      item: {name: 'Welcome to the ultimate DH Game!!!', discription: 'Have your drink ready'}
    }
  },
  methods: {
    submit() {
      this.nameList.push(this.i)
      this.i = null
    },
    restart () {
      this.list = this.bklist.slice();
      this.flag = 1;
      this.item = {name: 'Welcome to the ultimate DH Game!!!', discription: 'Have your drink ready'};
    },
    next() {
      this.item = this.list[Math.floor(Math.random()*this.list.length)]
      this.item.discription = this.item.discription.replace('$name', this.nameList[Math.floor(Math.random()*this.nameList.length)])
      this.item.discription = this.item.discription.replace('$name', this.nameList[Math.floor(Math.random()*this.nameList.length)])
      var i = this.item
      this.flag = 0;
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
  color: #000000;
  font-size: 2em;
}
spam {
  color:black;
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
.home {
    background-color: red;
    height: 100vh;
  }
img {
    width: 100px
}
input {
  padding: 0.5em;
  margin: 1em;
  border-radius: 50px;
  background-color: rgb(106, 106, 214);
  color: white;
  border: 3px solid rgb(0, 0, 0);
}
::placeholder { /* Chrome, Firefox, Opera, Safari 10.1+ */
  color: rgb(0, 0, 0);
  opacity: 1; /* Firefox */
}

:-ms-input-placeholder { /* Internet Explorer 10-11 */
  color: rgb(0, 0, 0);
}

::-ms-input-placeholder { /* Microsoft Edge */
  color: rgb(0, 0, 0);
}
.submit {
  font-size: 5px;
  margin-top: 1em;
  border-radius: 50px;
  background-color: rgb(53, 228, 0);
  color: white;
  padding: 1em;
  border: 1px ridge grey;
}
.nameList {
  color: black;
  font-size: 5px;
}
.restartButton {
  font-size: 20px;
  margin-top: 1em;
  border-radius: 50px;
  background-color: rgb(17, 0, 255);
  color: rgb(0, 0, 0);
  padding: 1em;
}
/*<spam>Player: &nbsp;</spam>*/
</style>
