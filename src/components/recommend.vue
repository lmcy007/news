<template>
  <div class="container">
    <carousel></carousel>
    <div class="article"  v-for="(item,i) in previewList">
      <div class="piece">
    <div class="title">
      {{i}}{{item.title}}
    </div>
        <div><span class="time">{{item.time}}</span></div>
    <div class="info">
      {{item.info}}
    </div>
    </div>
      <!--<div class="righttupian"><img src="../assets/tuijian/tupian0.jpg" alt="Readhub" ></div>-->
  </div>
    <div align="center" class="ceshi"><button class="button0"  @click.asyc="monclickbutton"> 加载更多 </button></div>
  </div>
</template>

<script  type="text/javascript">
  /* eslint-disable semi,indent */

  import Vue from 'vue'
  import VueResource from 'vue-resource'
  Vue.use(VueResource);
  import { mapState } from 'vuex'
  // vuex常量
  import * as getProdListData from '../store/types/getProdListData-types'
  import carousel from '@/components/carousel'
  export default {
    name: 'Recommend',
    data: function () {
      return {
        item: '',
        index: '',
        previewList: []
      }
    },
    components: {
      carousel
    },
    mounted: function () {
      this.getHottopicsReset();
    },
    methods: {
      monclickbutton(){
        this.getHottopics();
      },
      getHottopicsReset: function () {
        var _this;
        _this = this;
        this.$store.dispatch(getProdListData.ADD_PRODLISTDATA_ACTION_RESET).then(() => {
          this.previewList = this.prodListData;
        });
      },
      getHottopics: function () {

        var _this = this
        this.$store.dispatch(getProdListData.ADD_PRODLISTDATA_ACTION).then(() => {
          this.previewList = this.prodListData;
        });
      },
      toggle: function (item) {
        item.show = !item.show
      }
    },
    computed:mapState({ //vuex 状态
      prodListData: state => state.getProdListData.prodListData
    })
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .container{
    font-size:1em;
    margin-top:1em;
    width:30rem;
    align-items: center;
    margin:0 auto;
    background:#ffffff;
  }
  .article{
    border-bottom: 1px solid #dddddd;
    font-size:0.1em;
    text-align: left;
    padding-top:5em;
    padding-bottom:1em;
  }
  .piece{
    width:20rem;
  }
  .title{
    position: relative;
    padding-left: 1em;
    line-height: 1.5em;
    color: #545454;
    font-weight: 500;
    cursor: pointer;
    font-size:11em;
    clear: both;
    -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
  }
  .title a{
    text-decoration:none;
  }
  .time{
    font-size: 10px;
    color: #aaacb4;
    line-height: 3em;
    padding-left: 2em;
  }
  .button0 {
    background-color: white;
    font-size: 14px;
    color: black;
    border-radius: 4px;
    width: 30%;
    height:50%;
    border: 0px solid #0099ff; /* Green */
    margin-top:1em;
    margin-bottom: 1em;
    outline:none ;
  }
   .info{
    font-size: 8em;
    line-height: 1.8em;
    color: #aaacb4;
     padding-left: 1.3em;
  }
  .detail{
    font-size:1em;
  }
  .righttupian{
    width:2rem;
    float:right;
  }
</style>
