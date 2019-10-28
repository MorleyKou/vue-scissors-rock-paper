<template>
  <div id="app">
    <header id="hd">
       Result : Win - ({{winCount}}) 
       , Lose - ({{loseCount}}) 
       , Draw - ({{drawCount}}) 
       <button @click="()=> reset()" >Reset</button>
    </header>
    <div id="bot-placeholder" >
      <img :src="bot_image">
    </div>
    <div id="you-placeholder" >
      <img :src="you_image">
    </div>
    <div id="buttons-container" >
      <div id="btn-paper" @click="()=> userPicked(1)"></div>
      <div id="btn-scissor" @click="()=> userPicked(2)"></div>
      <div id="btn-rock" @click="()=> userPicked(3)"></div>
    </div>
<!--     <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
    //HelloWorld
  },
  data() {
    return {
      botChoice: 0,
      userChoice: 0,
      winCount: 0,
      loseCount: 0,
      drawCount: 0,
    }
  },
  methods:{
    reset() {
      this.winCount=0;
      this.loseCount=0;
      this.drawCount=0;
      this.botChoice=0;
      this.userChoice=0;
    },
    userPicked(userPicked) {
      let botPicked = Math.floor(Math.random()*3)+1;

      if (userPicked == botPicked) {
        this.botChoice = botPicked + 100;
        this.userChoice = userPicked + 100;
        this.drawCount+=1;
      } else if (
        userPicked ==1 && botPicked ==3 ||
        userPicked ==2 && botPicked ==1 ||
        userPicked ==3 && botPicked ==2 
        ) {
        this.botChoice = botPicked * -10;
        this.userChoice = userPicked * 10 ;
        this.winCount+=1;
      } else if ( 
        userPicked == 1 && botPicked == 2 || 
        userPicked == 2 && botPicked == 3 || 
        userPicked == 3 && botPicked == 1 ) {
        this.botChoice = botPicked * 10;
        this.userChoice = userPicked * -10;
        this.loseCount+=1;
      }
    }
  },
  computed: {
    bot_image() {
      let botChoice={};
      botChoice['-30'] = 'rock-lose.png';
      botChoice['-20'] = 'scissor-lose.png';
      botChoice['-10'] = 'paper-lose.png';
      botChoice['0'] = 'Placeholder-Bot.png';
      botChoice['30'] = 'rock-win.png';
      botChoice['20'] = 'scissor-win.png';
      botChoice['10'] = 'paper-win.png';
      botChoice['103'] = 'rock-draw.png';
      botChoice['102'] = 'scissor-draw.png';
      botChoice['101'] = 'paper-draw.png';

      return `/images/${botChoice[this.botChoice]}`;
    },
    you_image() {
      let userChoice={};
      userChoice['-30'] = 'rock-lose.png';
      userChoice['-20'] = 'scissor-lose.png';
      userChoice['-10'] = 'paper-lose.png';
      userChoice['0'] = 'Placeholder-You.png';
      userChoice['30'] = 'rock-win.png';
      userChoice['20'] = 'scissor-win.png';
      userChoice['10'] = 'paper-win.png';
      userChoice['103'] = 'rock-draw.png';
      userChoice['102'] = 'scissor-draw.png';
      userChoice['101'] = 'paper-draw.png';

      return `/images/${userChoice[this.userChoice]}`;
    },
    // winCount() {
    //   return 0;
    // },
    // loseCount() {
    //   return 0;
    // },
    // drawCount() {
    //   return 0;
    // }
  }
}
</script>

<style>
#app {
  /*font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;*/
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
  background-color: #44D7B6;
}

#bot-placeholder , #you-placeholder {
  flex: 0px 2 1;
  padding: 20px 0;
}

#buttons-container {
  flex: 0px 1 1;
  display: flex;
  flex-direction: row;
}

#bot-placeholder img, #you-placeholder img {
  display:block;
  width: 60%;
  height: auto;
  margin: auto;
}


#buttons-container div {
  flex: 0px 1 1;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center bottom;
}

#btn-paper {
  background-image: url('/images/paper-btn.png');
}
#btn-scissor {
  background-image: url('/images/scissor-btn.png');
}
#btn-rock {
  background-image: url('/images/rock-btn.png');
}

header {
  background-color: #000000;
  padding: 10px 10px;
  color: #FFFFFF;
}
</style>
