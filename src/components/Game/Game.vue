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
    <div v-if="status===true" v-once>
      <Enemy
        v-for="(e, index) in totalEnemy"
        :key="index"
        :increaseScore="increaseScore"
        :decreaseLife="decreaseLife"
        :style="{
          position: 'absolute',
          top: `${getRandomInt(15, 75)}vh`,
          left: `${getRandomInt(20, 80)}vw`,
        }"
      />
      
    </div>
    <div v-if="!isAlive" class="gameover">
      <div class="gameoverTxt">Game Over</div>
      <button @click="start" class="restartBtn">Restart</button>
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
      totalEnemy: null,
      timer: null,
      flashTimer: null,
      status: null,
    }
  },
  methods: {
    getRandomInt: function(min, max) {
      return Math.floor(Math.random() * (max - min)) + min;
    },
    increaseScore: function(){
      this.score += 1
    },
    decreaseLife: function(){
      this.lifes -= 1
      this.backgroundFlash = 'red'
      this.flashTimer = setTimeout(()=>{
        this.backgroundFlash = 'black'
      }, 250)
    },
    start: function(){
      this.status = true
      this.lifes = 3
      this.score = 0
      this.totalEnemy = 30
    },
  },
  computed: {
    isAlive: function (){
      if(!(this.lifes > 0))
        this.status = false
      return this.lifes > 0 && this.status
    },
  },
  mounted(){
    this.start()
  },
  beforeDestroy (){
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