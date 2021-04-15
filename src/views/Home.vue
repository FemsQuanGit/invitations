<template>
  <div class="home">
    <night-scene/>
  </div>
</template>

<script>
import NightScene from '../components/nightScene.vue'
export default {
  name: 'Home',
  components:{
    NightScene
  },
  mounted(){
  }
}
</script>

<style lang="scss" scoped>
.home{
  height: 100%;
  width: 100%;
}
</style>
