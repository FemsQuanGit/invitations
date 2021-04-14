<template>
  <div class="home">
    <div v-for="i in 15" :key="i" :class="`item${i}`"></div>
  </div>
</template>

<script>
import anime from 'animejs/lib/anime.es.js'
export default {
  name: 'Home',
  data(){
    return {
    }
  },
  mounted(){
    this.startAnime()
  },
  methods:{
    startAnime(){
      const targetsArr = []
      for (let i = 1; i <= 15; i++) {
        targetsArr.push(`.item${i}`)
      }
      anime({
        targets: targetsArr,
        opacity: [0,1],
        direction: 'alternate',
        duration: 10000,
        loop: true,
        easing: 'easeInOutCubic',
        delay: anime.stagger(5000)
      })
    }
  }
}
</script>

<style lang="scss" scoped>
@mixin div-background($index) {
  position: absolute;
  height: 100%;
  width: 100%;
  background-image: url('../assets/#{$index}.jpg');
  background-size: 100% 100%;
  background-repeat: no-repeat;
}
.home{
  position: relative;
  height: 100%;
  width: 100%;
  background-image: url('../assets/bg.jpg');
  background-size: 100% 100%;
  background-repeat: no-repeat;
  @for $i from 1 through 15 {
    .item#{$i} {  @include div-background($i); }
  }
}
</style>
