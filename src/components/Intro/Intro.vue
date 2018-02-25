<template>
  <div class="container">
    <div class="title">
      개발자 소개
    </div>
    <span class="sd">
      SOFTWARE DEVELOPER
      </span>
    <span class="name">
      정보석 (만 25세)
    </span>
    <div class="row">
      <div class="leftWrapper">
        <div class="subtitle">Contact</div>
        boseokjung@gmail.com<br />
        010-8685-2005<br />
        <a href="https://github.com/jewelism">https://github.com/jewelism</a>
        서울시 구로구 신도림동
      </div>
      <div class="rightWrapper">
        <div class="subtitle">Education</div>
        강서고등학교<br />
        성공회대학교<br />
        소프트웨어공학 전공<br />
        2018년 8월 졸업 예정
      </div>
    </div>
    
    <div class="graphWrapper">
      <span class="subtitle">Skills</span>
        <div v-for="(s, index) in skills" class="graphItem">
          <span class="skillName">{{s.name}}</span>
          <span class="skillBar">
            <ProgressBar :percentage="s.per" :index="index" />
          </span>
        </div>
    </div>
  </div>
</template>

<script>
import ProgressBar from '../Common/ProgressBar'

export default {
  name: 'Intro',
  data(){
    return {
      skills: [
        { name: 'HTML', per: 75 },
        { name: 'CSS', per: 60 },
        { name: 'Java', per: 85 },
        { name: 'Spring', per: 75 },
        { name: 'node.js', per: 75 },
        { name: 'ES6', per: 90 },
        { name: 'react.js', per: 90 },
        { name: 'RN', per: 90 },
        { name: 'vue.js', per: 85 },
      ]
    }
  },
  components: {
    ProgressBar
  }
} 
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 5vw;
  margin-bottom: 5vw;
}

.title {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-size: 30px;
}

.sd {
  font-size: 20px;
  margin-top: 50px;
}

.row {
  display: flex;
  flex-direction: row;
  justify-content: center;
  width: 100vw;
}

.leftWrapper {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  text-align: right;
  margin-right: 2vw;
  width: 35vw;
}

.rightWrapper {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  text-align: left;
  margin-left: 2vw;
  width: 35vw;
}

.subtitle {
  font-style: bold;
  font-size: 20px;
  margin-bottom: 10px;
}

.name {
  font-size: 22px;
  margin: 20px;
  border-bottom: 1px solid black;
}

.graphWrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 500px;
  margin-top: 30px;
}

.graphItem {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  width: 100%;
  // padding-left: 10px;
  margin-bottom: -10px;
}

.skillName {
  width: 30%;
}

.skillBar {
  width: 70%;
}

@media (max-width: 400px) {
  .sd {
    font-size: 15px;
    margin-top: 20px;
  }

  .name {
    font-size: 20px;
    margin: 15px;
    border-bottom: 1px solid black;
  }

  .graphWrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 350px;
    margin-top: 15px;
  }

  .skillName {
    width: 75px;
  }

  .row {
    font-size: 12px;
    /* border:1px solid black; */
  }

  .subtitle {
    font-style: bold;
    font-size: 15px;
    margin-bottom: 5px;
  }
}
</style>
