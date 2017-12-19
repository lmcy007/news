<template lang="html">
  <div class="carousel">
    <transition-group tag="ul" name="image" class="clearfix">
        <li v-for="(item, index) in slides" :key="index" v-show="index===nowIndex">
          <img :src="item.src" width="100%" height="100%">
        </li>
      </transition-group>
      <div class="bullet">
        <span v-for="(item,index) in slides.length" :class="{active:index===nowIndex}"></span></div>
    </div>
</template>

<script>
export default {
  created() {
    this.play()
  },
  data() {
    return {
      nowIndex: 0,
      slides: [
        {src: require('../assets/redian/chaoxian.jpg')},
        {src: require('../assets/redian/Is.jpg')},
        {src: require('../assets/redian/ouzhou.jpg')},
        {src: require('../assets/redian/wanda.jpg')},
        {src: require('../assets/redian/waijiaobu.jpg')},
      ]
    }
  },
  methods: {
    autoPlay() {
      this.nowIndex++
      if(this.nowIndex === 5) {
      this.nowIndex = 0
      return
      }
    },
    play() {
      setInterval(this.autoPlay, 4000)
    }
  }
}
</script>

<style lang="css" scoped>
.carousel {
  text-align:center;
  width:30rem;
  height: 10rem;
  line-height:2.5rem;

  text-align:center;
  color: white;
  font-family: "宋体";
  font-style: italic;
  font-size:25px;
  margin:0 auto;

}
li {
  position: absolute;
}
li img {
  width:30rem;
  height: 10rem;
}
.image-enter-active {
  transform: translateX(10);
  transition: all 1s ease;
}
.image-leave-active {
  transform: translateX(0);
  transition: all 1s ease;
}
.image-enter {
  transform: translateX(0);
}
.image-leave {
  transform: translateX(0);
}
.bullet {
  position: absolute;
  top: 12rem;
  right:21rem;
  margin: 0 auto;
  text-align: right;
  z-index: 10;
}
.bullet span {
  width: 10px;
  height: 10px;
  border: 1px solid;
  display: inline-block;
  margin-right: 10px;
  border-radius: 10px;
}
.active {
  background-color: #f00;
}
.clearfix {
  content: '';
  clear: both;
  display: block;
}
</style>
