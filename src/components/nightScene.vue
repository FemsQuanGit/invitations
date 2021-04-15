<template>
  <!-- 夜景图片渐影渐现 -->
  <div class="night-scene">
    <div v-for="i in 12" :key="i" :class="`item${i}`"></div>
		<div @click="onClickMusic" class="radio-button"></div>
    <audio ref="music" src="../assets/music/night.mp3" type="audio/mpeg" autoplay loop />
  </div>
</template>

<script>
// 引入animejs动画库
import anime from 'animejs/lib/anime.es.js'
export default {
  name: 'NightScene',
	data(){
		return {
			musicAnimation:null,
			pictureAnimatation:null
		}
	},
  mounted(){
    this.initAnimation()
  },
  methods:{
		initAnimation(){
			// 音频动画
			this.musicAnimation = anime({
				targets:'.radio-button',
				rotate: 360,
				easing:'linear',
				loop: true
			})
			// 组装动画目标选择器-图片动画
      const targetsArr = []
      for (let i = 1; i <= 12; i++) {
        targetsArr.push(`.item${i}`)
      }  
      this.pictureAnimatation = anime({
        targets: targetsArr,
        opacity: [0,1],//动画属性，透明度0~1
        direction: 'alternate',//动画方向一去一回
        duration: 10000,//动画周期10s
        loop: true,//循环动画
        easing: 'easeInOutCubic',//动画曲线
        delay: anime.stagger(5000)//每个动画系列延迟5s执行
      })
		},
		onClickMusic(){
			if(this.$refs.music.paused){
				this.musicAnimation.play()
				this.$refs.music.play()
			} else{
				this.musicAnimation.pause()
				this.$refs.music.pause()
			}
		}
  }
}
</script>

<style lang="scss" scoped>
@mixin div-background($index) {
  position: absolute;
  height: 100%;
  width: 100%;
  background-image: url('../assets/night_scene/#{$index}.jpg');
  background-size: 100% 100%;
  background-repeat: no-repeat;
}
.night-scene{
  position: relative;
  height: 100%;
  width: 100%;
  background-image: url('../assets/night_scene/1.jpg');
  background-size: 100% 100%;
  background-repeat: no-repeat;
  @for $i from 1 through 12 {
    .item#{$i} {  @include div-background($i); }
  }
	.radio-button{
		position: absolute;
		height: 30px;
		width: 30px;
		background-image: url('../assets/music/music.png');
		background-repeat: no-repeat;
		background-size: 100% 100%;
		right: 5px;
		top: 5px;
		z-index: 99;
	}
}
</style>
