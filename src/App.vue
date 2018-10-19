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
    <Moles :moles='moles' :isActive='gameActive'></Moles>
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
      this.resetData();
      this.timerId = setInterval(this.startTimer, 1000);
    },
    endGame: function(){
      this.gameActive = false;
      clearInterval(this.timerId);
    },
    startTimer: function(){
      this.timer -= 1;
      if (this.timer === 0){
        this.endGame();
      }
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
