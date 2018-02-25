<template>
  <div v-if="status" class="enemy">
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
      timer: null,
    }
  },
  methods: {
    onClickHead: function () {
      this.life = 0
    },
    onClickBody: function () {
      this.life--
    },
  },
  computed: {
    status: function(){
      if(this.life > 0){
        return true
      } else {
        this.increaseScore()
        clearTimeout(this.timer)
        return false
      }
    }
  },
  mounted () {
    this.timer = setTimeout(()=>{
      this.decreaseLife()
    }, 3000)
  },
  destroyed (){
    clearTimeout(this.timer)
  }
}
</script>

<style scoped>
.enemy {
  position: absolute;
  left: 50%;
  right: 50%;
  width: 10px;
  height: 17px;
  background-color: red;
  z-index: 1;

  animation: ani 1000s;
  // animation: ani 200s 1 forwards;
}

@keyframes ani { 
  from { }
  to { width: 1000%; height: 1700% }
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