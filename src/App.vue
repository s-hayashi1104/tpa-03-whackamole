<template>
  <div class="whackamole">
    <h1 class="logo">
      Whack-a-mole!
    </h1>
    <button
      class="start-game"
    @click= "startGame">
      Start Game
    </button>
    <div class="counters-container">
      <Counter title='score' :value="score" ></Counter>
      <Counter title='highScore' :value="highScore"></Counter>
      <Counter title='timer' :value="timer"></Counter>
    </div>
    <Moles :moles='moles' :isActive='gameActive' @whack="whackMole"></Moles>
  </div>
</template>

<script>
import Counter from './components/Counter';
import Moles from './components/Moles';
export default {
  name: 'App',
  components: {
    Counter,
    Moles,
  },
  methods:{
    resetData: function(){
      this.score = 0;
      this.timer = 20;
      this.moles =  [false, false, false, false];
      this.gameActive = true;
    },
    startGame: function(){
      if (this.gameActive) {
        return;
      }
      this.resetData();
      this.timerId = setInterval(this.startTimer, 1000);
      this.appear();
    },
    endGame: function(){
      this.gameActive = false;
      clearInterval(this.timerId);
      this.stop();
      this.updateHighScore();
    },
    updateHighScore() {
      this.highScore = Math.max(this.highScore, this.score);
    },
    startTimer: function(){
      this.timer -= 1;
      if (this.timer === 0){
        this.endGame();
      }
    },
    appear: function() {
      this.moleInterval = setInterval(this.randomMole.bind(this), 500);
    },
    stop: function() {
      clearInterval(this.moleInterval);
    },
    randomMole: function() {
      const randomMoleIndex = Math.floor(Math.random() * this.moles.length);
      if (!this.moles[randomMoleIndex]) {
        this.active(randomMoleIndex);
      }
    },
    toggle: function(moleId, appearMole) {
      const moles = this.moles.slice();
      moles[moleId] = appearMole;
      this.moles = moles;
    },
    active: function(moleId) {
      this.toggle(moleId, true);
      setTimeout(() => this.deactive(moleId), 1500);
    },
    deactive: function(moleId) {
      this.toggle(moleId, false);
    },
    whackMole: function(moleId) {
      this.score = this.score + 1;
      this.deactive(moleId);
    },
  },
  data: function() {
    return {
      score: 0,
      highScore: 0,
      timer: 20,
      timerId: 0,
      moles: [false, false, false, false],
      gameActive: false,
    };
  },
};
</script>

<style scoped>
.whackamole {
  font-family: 'Bungee', sans-serif;
  max-width: 960px;
  margin: auto;
  text-align: center;
}

.start-game {
  font-family: 'Bungee', sans-serif;
  padding: 20px;
  border-radius: 3px;
  border: 0;
  background-color: #52b1d6;
  color: #fff;
  font-size: 1em;
  cursor: pointer;
}

.counters-container {
  display: flex;
  justify-content: space-evenly;
}
</style>
