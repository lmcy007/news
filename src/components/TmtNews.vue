<template>
  <div id="containerID" class="container">
    <div v-bind:id="i" class="article" v-for="(item,i) in previewList" v-on:click="toggle(item),outlineart(item,item.show,i)">
      <div class="title">
        {{i}}{{item.name}}
       </div>
      <ul>
      <li class="info" v-for="(m,k) in item.article"  v-show="!item.show">
        <div>{{m.title}}</div>
      </li>
      </ul>
    </div>
    <div align="center"><button class="button0"  @click="monclickbutton"> 加载更多 </button></div>

  </div>

</template>

<script  type="text/javascript">
    import Vue from 'vue'
    import VueResource from 'vue-resource'
    Vue.use(VueResource)
    import { mapState } from 'vuex'

    // vuex常量
    import * as getProdListData from '../store/types/getProdListData-types'

    export default {
        name: 'TmtNews',
        data: function () {
            return {
                item:'',
                index:'',
                aId:"0",
                previewList: []
            }
        },
        components: {
        },
        mounted: function () {
                   this.getAuthorsRESET();
                    },
        methods: {
            monclickbutton(){
                this.getAuthors();
            },
            getAuthorsRESET:function(){
                var _this = this;
                this.$store.dispatch(getProdListData.ADD_AUTHORLISTDATA_ACTION_RESET).then(() => {
                    this.previewList = this.authorListData;
                });
            },
            getAuthors: function () {
                var _this = this;
                this.$store.dispatch(getProdListData.ADD_AUTHORLISTDATA_ACTION).then(() => {
                    this.previewList = this.authorListData;
                });
            },
            toggle: function (item) {
                item.show = !item.show;

                          },
            outlineart:function(item,a,i){

                for(var j=0;j<i;j++){

                    document.getElementById(j).style.border="none";
                    document.getElementById(j).style.borderRadius="0em";
                }
                for(var j=(i+1);j<this.previewList.length;j++){

                    document.getElementById(j).style.border="none";
                    document.getElementById(j).style.borderRadius="0em";
                }

                if(a==0){
                document.getElementById(i).style.border="thin solid #dddddd";
                   document.getElementById(i).style.borderRadius="1em";
                //document.getElementById("authorID").style.visibility='visible';

              }
             else{
              //      document.getElementById(i).style.borderRadius="0em";
                document.getElementById(i).style.border="none";
                    document.getElementById(i).style.borderRadius="0em";
             }
            },
            outlineart_rst:function(a,i){
                for(var j=0;j<previewList.length;j++){
                    document.getElementById(i).style.border="none";
                    document.getElementById(i).style.borderRadius="0em";
                }


            }

        },
        computed: {
            ...mapState({ //vuex 状态

                authorListData: state => state.getProdListData.authorListData

            })
        }
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
  .Newimg{
    float:right;
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
    text-decoration:none
  }
  .time{
    margin-left: 10px;
    font-size: 10px;
    color: #aaacb4;
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
    outline:0;
  }

  .info{
    margin-top: 5px;
    margin-left:2em;
    font-size: 14px;
    line-height: 1.8em;
    color: #aaacb4;
    border-radius:8px;
  }
  .detail{
    text-align:right;
    font-size:0.1em;
  }
  .addnews{

  }
</style>
