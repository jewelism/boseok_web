<template>
  <div :style="{
    display: 'flex',
    flexDirection: 'column',
    justifyContent: 'center',
    alignItems: 'center',
    marginBottom: '10vh',
  }">
    <Intro v-if="currentPage === 'Intro'"/>
    <Portfolio v-if="currentPage === 'Portfolio'"/>
    <Game v-if="currentPage === 'Game'"/>
    <div :style="{
      width: '100%',
      position: 'fixed',
      bottom: 0,
      paddingBottom: '4vh',
      backgroundColor: '#FFF',
      textAlign: 'center',
    }">
      <FooterMenu :onClickMenuItem="onClickMenuItem" />
    </div>
  </div>
</template>

<script>
import Intro from './components/Intro/Intro'
import Game from './components/Game'
import Portfolio from './components/Portfolio/Portfolio'
import FooterMenu from './components/FooterMenu'

export default {
  name: 'App',
  data(){
    return {
      currentPage: 'Intro',
    }
  },
  methods: {
    onClickMenuItem: function ({id, url}){
      if(url){
        location.href = url
      } else {
        this.currentPage = id
      }
    }
  },
  components: {
    Intro,
    Game,
    Portfolio,
    FooterMenu
  }
}
</script>
