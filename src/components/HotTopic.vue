<template>
  <div class="container">    
    <carousel></carousel>
    <div class="article"  v-for="(item,i) in previewList" v-on:click="toggle(item)">
    <div class="title">
      {{i}}{{item.title}}
      <span class="time">{{item.time}}</span>
    </div>
    <div class="info"  v-show="!item.show">
      {{item.info}}
      <div class="detail"><a href="http://mp.weixin.qq.com/s/ZdRnAIqx7r19Knbjc6Cirw">查看新闻</a>
      </div>
    </div>
  </div>
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
    name: 'HotTopic',
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
      getHottopicsReset: function () {
        var _this;
        _this = this;
        this.$store.dispatch(getProdListData.ADD_PRODLISTDATA_ACTION_RESET).then(() => {
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
  }
  .title{
    position: relative;
    padding-left: 1em;
    line-height: 3em;
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
    margin-left: 10px;
    font-size: 10px;
    color: #aaacb4;
  }
   .info{
    margin-top: 5px;
    font-size: 8em;
    line-height: 1.8em;
    color: #aaacb4;
  }
  .detail{
    text-align:right;
    font-size:1em;
  }
</style>
