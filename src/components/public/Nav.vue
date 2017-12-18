<template>
  <section class="nav">
    <!--v-for遍历路由-->
    <div class="nav" v-for='m in menus'>
      <router-link :to='setPaht(m.path)'><span>{{m.text}}</span></router-link>
    </div>
    <div>
      <img src="F:\nodejs\node_global\etc\news-temp\src\assets\head\add.png"/>
    </div>
    <!--<div class="aside">
      <div v-for='i in 3' class="line"></div>
    </div>-->
  </section>
</template>

<script>
export default {
  name: 'nav',
  data () {
    return {
      // 路由参数
      menus: [{
        text: '精选',
        path: '/select'
      }, {
        text: '热点',
        path: '/HotTopic'
      }, {
        text: '话题',
        path: '/point'
      }, {
        text: '作者',
        path: '/author'
      }, {
        text: '视频',
        path: '/shipin'
      }, {
        text: '军事',
        path: '/HotTopic'
      }, {
        text: '科技',
        path: '/keji'
      }]
    }
  },
  methods: {
    setPaht (path) {
      return path
    }
  }
}
</script>

<style lang="stylus">
.nav{
  width:30rem;
  height: 2.5rem;
  display: flex;
  justify-content: space-around;
  align-items: center;
  background: #fff;
  margin:0 auto;
  border-bottom: 1px solid #dddddd;
  .nav{
    width: 34%;
    height: 100%;
    a{
      height: 100%;
      width: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
      text-decoration: none;
      color: #666;
      font-size: 18px;
      text-align: center;
      span:first-child{
        height: 30px;
        width: 100%;
        line-height: 30px;
      }
    }
  }
  .aside{
    border solid;
    width:3rem;
    height: 2rem;
    cursor: pointer;
    position: absolute;
    top: 1em;
    right: 0;
    padding-top: 1px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    .line{
      height: 1px;
      width: 25px;
      background:#f00000;
      transition: all 0.5s;
    }
    .line:nth-of-type(2){
      margin: 6px 0;
    }
  }
  .line:nth-of-type(2){
    margin: 6px 0;
  }
  /*div:nth-child(2) > a > span{
    border-left: 1px solid #f00;
    border-right: 1px solid #eee;
  }
  div:nth-child(3) > a > span{
    border-left: 1px solid #eee;
    border-right: 1px solid #f00;
  }*/
  .active{
    border-bottom: 1px solid red;
    box-sizing: border-box;
  }
}
</style>
