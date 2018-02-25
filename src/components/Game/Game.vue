<template>
  <div class="game" :class="backgroundFlash">
    <div class="statusBarWrapper">
      <div class="statusBar">
        <div class="lifes">
          <span>Life : </span>
          <span>
            <img src="../../assets/heart.png" v-for="life in lifes" class="life"/>
          </span>
        </div>
        <div class="score">
          Score : {{score}}
        </div>
      </div>
    </div>
    <div v-if="status===true">
      <Enemy :increaseScore="increaseScore" :decreaseLife="decreaseLife"/>
    </div>
    <div v-if="!isAlive" class="gameover">
      <div class="gameoverTxt">Game Over</div>
      <button @click="restart" class="restartBtn">Restart</button>
    </div>
  </div>
</template>

<script>
import Enemy from './Enemy'

export default {
  name: 'Game',
  data(){
    return {
      backgroundFlash: 'black',
      lifes: 3,
      score: 0,
      enemy: 30,
      timer: null,
      flashTimer: null,
      status: null,
    }
  },
  methods: {
    increaseScore: function(){
      this.score ++
    },
    decreaseLife: function(){
      this.lifes --
      this.backgroundFlash = 'red'
      this.flashTimer = setTimeout(()=>{
        this.backgroundFlash = 'black'
      }, 250)
    },
    start: function(){
      this.status = true
      this.lifes = 3
      this.score = 0
      this.enemy = 30
    },
    restart: function(){
      this.start()
    }
  },
  computed: {
    isAlive: function (){
      return this.lifes > 0
    },
  },
  mounted(){
    this.start()
  },
  destroyed(){
    clearTimeout(this.timer)
  },
  components: {
    Enemy
  }
}
</script>

<style scoped>
.game {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 80%;
  height: 70vh;
  margin-top: 10vh;
  z-index: 0;
  cursor: url(https://www.iconfinder.com/icons/183165/download/png/128) !important;
}

.black {
  background-color: black;
}

.red {
  background-color: red;
}

.statusBarWrapper {
  position: fixed;
  top: 50px;
  width: 70vw;
  text-align: center;
}

.statusBar {
  // background-color: yellow;
  width: 100%;
  display: flex;
  justify-content: space-between;
  font-size: 20px;
}

.lifes {
  display: flex;
  justify-content: space-between;
}

.life {
  width: 20px;
  height: 20px;
  margin-top: -3px;
  margin-left: 10px;
}

.gameover { /* wrapper */
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.gameoverTxt {
  font-size: 40px;
  color: white;
  margin-bottom: 10px;
}

.restartBtn {
  width: 120px;
  height: 45px;
  border-radius: 15px;
  font-size: 18px;
}
</style>