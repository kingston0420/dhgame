<template>
  <div>
    <br>
    <spam>Number of Players:</spam>
    <input type="number" name="" v-model="i" placeholder="1" />
    <button class="submit" @click="submit()">Confirm</button>
    <p class="player">Player{{display}}'s turn</p>
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
    <button class="restartButton" @click="initNext()" v-if="flag == 1">Start Game</button>
    <button @click="next()" v-else-if="list.length > 0 && flag == 0">Next Card</button>
    <button class="restartButton" @click="restart()" v-else>Restart</button>
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
      i: 0,
      playerNum: 0,
      display: 1,
      name: null,
      bklist: [
      {id:1, name:'Hydrate', discription:'Drink one.'}, 
      {id:2, name:'Hydrate', discription:'Take 2 sips.'}, 
      {id:3, name:'Master', discription:'Everyone must call you master until the turn is back to you. Slip up = 1 drink.'}, 
      {id:4, name:'Hotseat', discription:'Everyone gets to ask you 3 questions altogether (not each). You must answer honestly, or drink 2 to skip'}, 
      {id:5, name:'Hotseat', discription:'Everyone gets to ask you 3 questions altogether (not each). You must answer honestly, or drink 2 to skip'}, 
      {id:6, name:'Hotseat', discription:'Everyone gets to ask you 3 questions altogether (not each). You must answer honestly, or drink 2 to skip'}, 
      {id:7, name:'Truth or drink', discription:'Name the top three most attractive people in DH or drink 2'}, 
      {id:8, name:'Truth or drink', discription:'Name the top three most attractive people in DH or drink 2'}, 
      {id:9, name:'Name the top three', discription:'Most savage OG execs.'}, 
      {id:10, name:'Name the top three', discription:'Most savage current execs.'}, 
      {id:11, name:'Name the person...', discription:'That has disappointed you the most. Give them a drink.'}, 
      {id:12, name:'Mates', discription:'Pick a buddy! They drink every time you do. Ends after it is your turn again.'}, 
      {id:13, name:'Soju vortex', discription:'JK finish whatever\'s in your glass.'},
      {id:14, name:'Vote!', discription:'Who is most likely to be caught as the spy/mafia? That person drinks 3 times :^)'}, 
      {id:15, name:'Vote!', discription:'Who is most likely to.... (fill in the blank)? That person drinks 2 times.'}, 
      {id:16, name:'Vote!', discription:'Who is most likely to piss off the DH president? That person drinks 2 times.'}, 
      {id:17, name:'Vote!', discription:'Who is most likely to piss off a DH teacher? That person drinks 2 times.'}, 
      {id:18, name:'STFU', discription:'Drink 1 or mute yourself until your next turn.'}, 
      {id:19, name:'STFU', discription:'Drink 1 or mute yourself until your next turn.'}, 
      {id:20, name:'Dance moves', discription:'You start with a move, next person does that move and adds a new one, keep adding new moves until someone messes up and that person has to drink :^)'}, 
      {id:21, name:'Categories', discription:'Category is: Kpop groups. Loser drinks 1.'}, 
      {id:22, name:'Nighty night~', discription:'Last person to jump on their bed drinks 2.'}, 
      {id:23, name:'Vote...', discription:'Most likely to black out at retreat. They drink 2.'}, 
      {id:24, name:'Vote...', discription:'Most likely to green out. They drink 2.'}, 
      {id:25, name:'Favourites', discription:'Choose your favourite dancer in the room. Give them a drink :)'}, 
      {id:26, name:'Dance to music only you can hear', discription:'Mute your mic, dance for 8 counts with the mic muted. Also have a drink because I\'m sorry'},
      {id:27, name:'Who\'s the Hardest?', discription:'Everyone has a minute to find the hardest alcohol they have. Once everyone presents their alcohol with the percentage listed, the person with the weakest alcohol must drink a shot of said alcohol.'}, 
      {id:28, name:'If you...', discription:'...took an online dance class this week, drink 1 shot'}, 
      {id:29, name:'Ha. Ha. Ha.', discription:'You have 15 seconds to make anyone in the game laugh. Whoever laughs first drinks one shot. If no one laughs, you drink 1 shot.'}, 
      {id:30, name:'Never have I ever...', discription:'Everyone says something they haven\'t done, going around in alphabetical order, starting from you. Drink if you have done it.'}, 
      {id:31, name:'Never have I ever...', discription:'Everyone says something they haven\'t done, going around in alphabetical order, starting from you. Drink if you have done it.'}, 
      {id:32, name:'Text', discription:'Go into your messages and text "Hey ;)" to the 6th person in your inbox. Drink 2 to skip.'}, 
      {id:33, name:'Moshi moshi', discription:'Put your phone on speaker. Call the 12th person in your phone contacts OR in your recents (we get to vote). Say "hello" repeatedly as if you can\'t hear until they hang up.'}, 
      {id:34, name:'You are on hold', discription:'Everyone calls you (give out ur # hoe). The first person to get through wins and can distribute 2 drinks.'}, 
      {id:35, name:'Categories', discription:'Songs used in DH Shows. Loser drinks 2.'}, 
      {id:36, name:'Categories', discription:'Past and present DH teachers. Loser drinks 3.'}, 
      {id:37, name:'If you...', discription:'...danced since being put in quarantine, give away a shot.'}, 
      {id:38, name:'Pass it on', discription:'If you are selected to drink, you may pick someone else to take it for you.'}, 
      {id:39, name:'Pass it on', discription:'If you are selected to drink, you may pick someone else to take it for you.'},
      {id:40, name:'If you...', discription:'If you watched Netflix today, drink 1 shot.'}, 
      {id:41, name:'If you...', discription:'...made a tiktok, drink 10. Just kidding take 2.'}, 
      {id:42, name:'If you...', discription:'...aren\'t wearing blue rn, DRINK 5 TIMES #dhpride'}, 
      {id:43, name:'Black out', discription:'Last person to turn off their video drinks twice.'}, 
      {id:44, name:'BYE BYE', discription:'Last person to turn off their video drinks twice.'}, 
      {id:45, name:'No Numbers', discription:'No saying numbers. You drink the number you say :) Ends after it is your turn again.'}, 
      {id:46, name:'If anyone...', discription:'...have been told by Richard to be sexier, drink 1'}, 
      {id:47, name:'Categories', discription:'Vancouver dance studios. Loser drinks 1.'}, 
      {id:48, name:'Categories', discription:'Category is: UBC dance clubs / teams. Loser drinks 2.'}, 
      {id:49, name:'Screen Heaven', discription:'At any time until your next turn, you can turn your video off and everyone else also has to turn their video off. Last person to turn video off drinks 3 times (like in King\'s cup).'}, 
      {id:50, name:'Screen Heaven', discription:'At any time until your next turn, you can turn your video off and everyone else also has to turn their video off. Last person to turn video off drinks 3 times (like in King\'s cup).'}, 
      {id:51, name:'If you..', discription:'...wear your team shirt when it is not required, drink 1'}, 
      {id:52, name:'If you...', discription:'...brought bubble tea to class instead of water, drink 1. You need to drink water.'},
      {id:53, name:'Search History', discription:'Screen share and show your browser history from yesterday, or drink 3.'}, 
      {id:54, name:'No Name Brand', discription:'No saying names until your turn comes again. Every person who does takes 1 drink each time.'}, 
      {id:55, name:'Consume!', discription:'The word "okay" cannot be said, or else you must drink 2. Ends once it is your turn again.'}, 
      {id:56, name:'Consume!', discription:'The word "drink" cannot be said, or else you must drink 2. Ends once it is your turn again.'}, 
      {id:57, name:'Consume!', discription:'The word "like" cannot be said, or else you must drink 2. Ends once it is your turn again.'}, 
      {id:58, name:'Categories', discription:'You choose! Loser drinks 2.'}, 
      {id:59, name:'The early bird is a tryhard...', discription:'If you got out of bed before 10am today, distribute 2.'}, 
      {id:60, name:'Freebies!', discription:'Distribute 2 drinks.'}, 
      {id:61, name:'Good bye', discription:'Completely disappear from the screen without touching your laptop or turning off your video. Last person to accomplish this drinks 2.'}, 
      {id:62, name:'Good bye', discription:'Completely disappear from the screen without touching your laptop or turning off your video. Last person to accomplish this drinks 2.'}, 
      {id:63, name:'Impersonation', discription:'You must impersonate someone in the chat - the first person to get it right may distribute 3 drinks.'}, 
      {id:64, name:'Have some water', discription:'No seriously, have a sip of water. Thanks.'}, 
      {id:65, name:'If you...', discription:'...have ever been a rep, give 1 drink. Thank you for what you have done for the club.'},
      {id:66, name:'Censorship', discription:'You choose a word to censor - anyone who says that word must sing the(ir) national anthem, and then take a drink after. Ends once it is your turn again.'}, 
      {id:67, name:'If you...', discription:'...made some sort of dalgona drink, drink 2.'}, 
      {id:68, name:'Blind guess', discription:'Pick someone in the chat. Guess their underwear colour. If you get it right, they drink 3. If you get it wrong, drink 3.'}, 
      {id:69, name:'If you...', discription:'...no longer have a job, drink 1. (I\'m sorry)'}
      ],
      list: [
      {id:1, name:'Hydrate', discription:'Drink one.'}, 
      {id:2, name:'Hydrate', discription:'Take 2 sips.'}, 
      {id:3, name:'Master', discription:'Everyone must call you master until the turn is back to you. Slip up = 1 drink.'}, 
      {id:4, name:'Hotseat', discription:'Everyone gets to ask you 3 questions altogether (not each). You must answer honestly, or drink 2 to skip'}, 
      {id:5, name:'Hotseat', discription:'Everyone gets to ask you 3 questions altogether (not each). You must answer honestly, or drink 2 to skip'}, 
      {id:6, name:'Hotseat', discription:'Everyone gets to ask you 3 questions altogether (not each). You must answer honestly, or drink 2 to skip'}, 
      {id:7, name:'Truth or drink', discription:'Name the top three most attractive people in DH or drink 2'}, 
      {id:8, name:'Truth or drink', discription:'Name the top three most attractive people in DH or drink 2'}, 
      {id:9, name:'Name the top three', discription:'Most savage OG execs.'}, 
      {id:10, name:'Name the top three', discription:'Most savage current execs.'}, 
      {id:11, name:'Name the person...', discription:'That has disappointed you the most. Give them a drink.'}, 
      {id:12, name:'Mates', discription:'Pick a buddy! They drink every time you do. Ends after it is your turn again.'}, 
      {id:13, name:'Soju vortex', discription:'JK finish whatever\'s in your glass.'},
      {id:14, name:'Vote!', discription:'Who is most likely to be caught as the spy/mafia? That person drinks 3 times :^)'}, 
      {id:15, name:'Vote!', discription:'Who is most likely to.... (fill in the blank)? That person drinks 2 times.'}, 
      {id:16, name:'Vote!', discription:'Who is most likely to piss off the DH president? That person drinks 2 times.'}, 
      {id:17, name:'Vote!', discription:'Who is most likely to piss off a DH teacher? That person drinks 2 times.'}, 
      {id:18, name:'STFU', discription:'Drink 1 or mute yourself until your next turn.'}, 
      {id:19, name:'STFU', discription:'Drink 1 or mute yourself until your next turn.'}, 
      {id:20, name:'Dance moves', discription:'You start with a move, next person does that move and adds a new one, keep adding new moves until someone messes up and that person has to drink :^)'}, 
      {id:21, name:'Categories', discription:'Category is: Kpop groups. Loser drinks 1.'}, 
      {id:22, name:'Nighty night~', discription:'Last person to jump on their bed drinks 2.'}, 
      {id:23, name:'Vote...', discription:'Most likely to black out at retreat. They drink 2.'}, 
      {id:24, name:'Vote...', discription:'Most likely to green out. They drink 2.'}, 
      {id:25, name:'Favourites', discription:'Choose your favourite dancer in the room. Give them a drink :)'}, 
      {id:26, name:'Dance to music only you can hear', discription:'Mute your mic, dance for 8 counts with the mic muted. Also have a drink because I\'m sorry'},
      {id:27, name:'Who\'s the Hardest?', discription:'Everyone has a minute to find the hardest alcohol they have. Once everyone presents their alcohol with the percentage listed, the person with the weakest alcohol must drink a shot of said alcohol.'}, 
      {id:28, name:'If you...', discription:'...took an online dance class this week, drink 1 shot'}, 
      {id:29, name:'Ha. Ha. Ha.', discription:'You have 15 seconds to make anyone in the game laugh. Whoever laughs first drinks one shot. If no one laughs, you drink 1 shot.'}, 
      {id:30, name:'Never have I ever...', discription:'Everyone says something they haven\'t done, going around in alphabetical order, starting from you. Drink if you have done it.'}, 
      {id:31, name:'Never have I ever...', discription:'Everyone says something they haven\'t done, going around in alphabetical order, starting from you. Drink if you have done it.'}, 
      {id:32, name:'Text', discription:'Go into your messages and text "Hey ;)" to the 6th person in your inbox. Drink 2 to skip.'}, 
      {id:33, name:'Moshi moshi', discription:'Put your phone on speaker. Call the 12th person in your phone contacts OR in your recents (we get to vote). Say "hello" repeatedly as if you can\'t hear until they hang up.'}, 
      {id:34, name:'You are on hold', discription:'Everyone calls you (give out ur # hoe). The first person to get through wins and can distribute 2 drinks.'}, 
      {id:35, name:'Categories', discription:'Songs used in DH Shows. Loser drinks 2.'}, 
      {id:36, name:'Categories', discription:'Past and present DH teachers. Loser drinks 3.'}, 
      {id:37, name:'If you...', discription:'...danced since being put in quarantine, give away a shot.'}, 
      {id:38, name:'Pass it on', discription:'If you are selected to drink, you may pick someone else to take it for you.'}, 
      {id:39, name:'Pass it on', discription:'If you are selected to drink, you may pick someone else to take it for you.'},
      {id:40, name:'If you...', discription:'If you watched Netflix today, drink 1 shot.'}, 
      {id:41, name:'If you...', discription:'...made a tiktok, drink 10. Just kidding take 2.'}, 
      {id:42, name:'If you...', discription:'...aren\'t wearing blue rn, DRINK 5 TIMES #dhpride'}, 
      {id:43, name:'Black out', discription:'Last person to turn off their video drinks twice.'}, 
      {id:44, name:'BYE BYE', discription:'Last person to turn off their video drinks twice.'}, 
      {id:45, name:'No Numbers', discription:'No saying numbers. You drink the number you say :) Ends after it is your turn again.'}, 
      {id:46, name:'If anyone...', discription:'...have been told by Richard to be sexier, drink 1'}, 
      {id:47, name:'Categories', discription:'Vancouver dance studios. Loser drinks 1.'}, 
      {id:48, name:'Categories', discription:'Category is: UBC dance clubs / teams. Loser drinks 2.'}, 
      {id:49, name:'Screen Heaven', discription:'At any time until your next turn, you can turn your video off and everyone else also has to turn their video off. Last person to turn video off drinks 3 times (like in King\'s cup).'}, 
      {id:50, name:'Screen Heaven', discription:'At any time until your next turn, you can turn your video off and everyone else also has to turn their video off. Last person to turn video off drinks 3 times (like in King\'s cup).'}, 
      {id:51, name:'If you..', discription:'...wear your team shirt when it is not required, drink 1'}, 
      {id:52, name:'If you...', discription:'...brought bubble tea to class instead of water, drink 1. You need to drink water.'},
      {id:53, name:'Search History', discription:'Screen share and show your browser history from yesterday, or drink 3.'}, 
      {id:54, name:'No Name Brand', discription:'No saying names until your turn comes again. Every person who does takes 1 drink each time.'}, 
      {id:55, name:'Consume!', discription:'The word "okay" cannot be said, or else you must drink 2. Ends once it is your turn again.'}, 
      {id:56, name:'Consume!', discription:'The word "drink" cannot be said, or else you must drink 2. Ends once it is your turn again.'}, 
      {id:57, name:'Consume!', discription:'The word "like" cannot be said, or else you must drink 2. Ends once it is your turn again.'}, 
      {id:58, name:'Categories', discription:'You choose! Loser drinks 2.'}, 
      {id:59, name:'The early bird is a tryhard...', discription:'If you got out of bed before 10am today, distribute 2.'}, 
      {id:60, name:'Freebies!', discription:'Distribute 2 drinks.'}, 
      {id:61, name:'Good bye', discription:'Completely disappear from the screen without touching your laptop or turning off your video. Last person to accomplish this drinks 2.'}, 
      {id:62, name:'Good bye', discription:'Completely disappear from the screen without touching your laptop or turning off your video. Last person to accomplish this drinks 2.'}, 
      {id:63, name:'Impersonation', discription:'You must impersonate someone in the chat - the first person to get it right may distribute 3 drinks.'}, 
      {id:64, name:'Have some water', discription:'No seriously, have a sip of water. Thanks.'}, 
      {id:65, name:'If you...', discription:'...have ever been a rep, give 1 drink. Thank you for what you have done for the club.'},
      {id:66, name:'Censorship', discription:'You choose a word to censor - anyone who says that word must sing the(ir) national anthem, and then take a drink after. Ends once it is your turn again.'}, 
      {id:67, name:'If you...', discription:'...made some sort of dalgona drink, drink 2.'}, 
      {id:68, name:'Blind guess', discription:'Pick someone in the chat. Guess their underwear colour. If you get it right, they drink 3. If you get it wrong, drink 3.'}, 
      {id:69, name:'If you...', discription:'...no longer have a job, drink 1. (I\'m sorry)'}
      ],

      item: {name: 'Welcome to the ultimate DH Game!!!', discription: 'Have your drink ready'}
    }
  },
  methods: {
    submit() {
      this.playerNum = Number(this.i);
    },
    initNext() {
      this.item = this.list[Math.floor(Math.random()*this.list.length)]
      this.flag = 0;
    },
    restart () {
      this.list = this.bklist.slice();
      this.flag = 1;
      this.item = {name: 'Welcome to the ultimate DH Game!!!', discription: 'Have your drink ready'};
      this.display = 1;
    },
    next() {
      this.display = (this.display)% (this.playerNum) + 1;
      this.item = this.list[Math.floor(Math.random()*this.list.length)]
      this.flag = 0;
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
  color:saddlebrown;
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
  background-color: #748cab;
}
button {
  font-size: 20px;
  margin-top: 1em;
  border-radius: 50px;
  background-color: rgb(0, 0, 0);
  color: white;
  padding: 1em;
  border: 2px solid grey;
}
.restartButton {
  font-size: 20px;
  margin-top: 1em;
  border-radius: 50px;
  background-color: #824670;
  color: rgb(0, 0, 0);
  padding: 1em;
}
spam {
  font-size: 1em;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  color:rgb(255, 255, 255);
}
.submit {
  font-size: 2px;
  margin: 0em 1em;
  border-radius: 0px;
  background-color: #824670;
  color: white;
  padding: 1em;
  border: 1px solid grey;
}
input {
  width: 5em;
  padding: 0.2em 1em;
  margin: 0em 1em;
  border-radius: 50px;
  background-color: rgb(106, 106, 214);
  color: white;
  border: 2px solid rgb(0, 0, 0);
}
.player {
  margin: 6px auto;
  font-size: 1.2em;
  color:rgb(255, 255, 255);
}

</style>
