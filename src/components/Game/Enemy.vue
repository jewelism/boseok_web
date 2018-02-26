<template>
  <div v-if="isAlive" :class="['enemy_' + index]" v-once>
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
    index: Number,
    increaseScore: Function,
    decreaseLife: Function,
    randomInt: Number,
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
    // console.log(this.randomInt)
    const createdStyleTag = document.createElement("style");
    const index = this.index;
    const animationName = `enemy_ani${index}`;
    createdStyleTag.textContent = `
      .enemy_${index} {
        width: 10px;
        height: 17px;
        background-color: red;
        z-index: ${50000-this.randomInt};

        animation: ${animationName} ${this.randomInt/20}s;
      }

      @keyframes ${animationName} { 
        from { }
        to { width: 10000px; height: 17000px }
      }
    `
    document.body.appendChild(createdStyleTag)

    this.enemy_timer = setTimeout(()=>{
      this.decreaseLife()
      this.isAlive = false
    }, this.randomInt)
  },
  beforeDestroy (){
    clearTimeout(this.enemy_timer)
  },
}
</script>

<style scoped>
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