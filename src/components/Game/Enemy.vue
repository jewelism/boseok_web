<template>
  <div v-if="isAlive" class="enemy" v-once>
    <div @click="onClickHead" class="enemy_head">
    </div>
    <div @click="onClickBody" class="enemy_body">
    </div>
  </div>
</template>

<script>
export default {
  name: 'Enemy',
  props: {
    increaseScore: Function,
    decreaseLife: Function,
  },
  data(){
    return {
      life: 3,
      isAlive: true,
    }
  },
  methods: {
    onClickHead: function () {
      this.life = 0
    },
    onClickBody: function () {
      this.life -= 1
    },
  },
  watch: {
    life: function(newVal){
      if(newVal <= 0){
        this.increaseScore()
        this.isAlive = false
      }
    }
  },
  mounted () {
    this.enemy_timer = setTimeout(()=>{
      this.decreaseLife()
      this.isAlive = false
    }, 20000)
  },
  beforeDestroy (){
    clearTimeout(this.enemy_timer)
  }
}
</script>

<style scoped>
.enemy {
  width: 10px;
  height: 17px;
  background-color: red;
  z-index: 1;

  animation: ani 1000s;
}

@keyframes ani { 
  from { }
  to { width: 10000px; height: 17000px }
}

.enemy_head {
  width: 100%;
  height: 35%;
  background-color: blue;
}

.enemy_body {
  width: 100%;
  height: 65%;
  background-color: gray;
}
</style>