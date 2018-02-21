<template>
  <div>
    <BasicBtn v-for="(item, index) of menuItems" :onClick="onClickMenuItem" :key="item.id" :param="{ id: item.id, url: item.url}" :value="item.display"/>
  </div>
</template>

<script>
import BasicBtn from './Common/BasicBtn'

export default {
  name: 'FooterMenu',
  props: {
    onClickMenuItem: {
      type: Function
    },
  },
  data(){
    return {
      menuItems: [
        { id: 'Intro', display: '개발자소개' },
        { id: 'Portfolio', display: '포트폴리오', url: 'portfolio.html' },
        // { id: 'Game', display: '게임' },
      ]
    }
  },
  components: {
    BasicBtn
  }
} 
</script>
