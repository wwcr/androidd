<!--页面css样式-->
<style scoped lang='scss'>
    .message {
        background: #f0f4fa;
        padding-top: 1.5rem;
        height: 100%;
    }

    .message1 {
        background: url('../../assets/img/no-msg.png') center;
        background-size:100%;
    }

    .message ul {
        background: #fff;
        margin-bottom: 1.5rem;
        margin-top: 0.2rem;
    }

    .message ul li {
        margin-left: 0.15rem;
        border-bottom: 1px solid #f1f1f1;
        padding: 0.1rem 0 0.3rem 0;
        // height:60px;
        margin-right: 0.15rem;
        box-sizing: border-box;
    }
    // .message ul li:nth-last-of-type(1) {
    //     border:none;
    // }
    .message ul li .img {
        float: left;
        margin-right: 0.3rem;
        position: relative;
    }

    .message ul li .img img {
        width: 1.7rem;
        height: 1.7rem;
        // margin-bottom:5px;
    }

    .message ul li .mess {
        display: inline-block;
        margin-top: 0.1rem;
    }

    .message ul li h5 {
        font-size: 0.32rem;
    }

    .message ul li .p1 {
        font-size: 0.35rem;
        color: #787878;
        padding-top: 0.1rem;
    }

    .message ul li .p2 {
        font-size: 0.35rem;
        color: #787878;
        margin-top: 0.2rem;
    }
    .img i{
      width: 0.3rem;
      height: 0.3rem;
      background: red;
      position: absolute;
      right: 0.1rem;
      top: 0;
      border-radius: 50%;
    }
    .mess h5{
        font-size: 0.4rem!important;
        font-weight: 400;
    }
    /*#ul .mint-cell-value{
        display: none !important;

    }*/
    .message ul li .img{
        margin-left: -10rem !important;
    }
    .message ul li .mess{
        margin-left: 0.3rem !important;
    }
    .mint-cell-swipe-button{
        font-size: 10px !important;
    }
    .mint-cell:last-child{
        background-image: linear-gradient(180deg,#fff,#fff 50%,transparent 0)!important;
    }
    .mess{
        width: 7rem!important;
        .p1{
            overflow:hidden;
            text-overflow:ellipsis;
            white-space:nowrap
        }
    }
    // .yo-scroll{
    //     top: 1.5rem !important;
    // }
    // 加载的loading样式
    .loading-icon{
        text-align: center;
        padding: .2rem 0 .4rem 0;
        img{
            width: .45rem;
            height: auto;
        }
    }
    .loading-img{
        width: .4rem;
        height: auto;
    }
    .warning-box{
        text-align: center;
        font-size: .4rem;
        margin-top: .5rem;
    }
    // 加载的loading样式结束
</style>
<!--服务列表-->
<template>
    <div class="message" :class="{message1 :noMsg}" v-if='info' 
        v-infinite-scroll="loadMore"
        infinite-scroll-disabled="loading"
        infinite-scroll-distance="1"
        infinite-scroll-immediate-check=false>
        <mt-loadmore 
                :top-method="loadTop" 
                @top-status-change="handleTopChange"
                ref="loadmore">
                <div slot="top" class="mint-loadmore-top">
                    <!-- 下拉刷新状态提示语 -->
                    <span v-show="topStatus == 'drop'" style="font-size: .3rem;">释放立即刷新</span>
                    <span v-show="topStatus == 'loading'" ><img class="loading-img" src="../../assets/img/loading.gif" alt=""></span>
                    <span v-show="topStatus == 'pull'" style="font-size: .3rem;">下拉刷新</span>
                </div>
        
            <ul v-if="info.length > 0" id="ul">
                <li v-for="(x,k) in info" @click="getContent(x.rid, x.mid, x, k)">
                    <mt-cell-swipe
                      :right="[
                        {
                          content: '删除',
                          style: { background: '#ff4040', color: '#fff', fontSize:'0.5rem', width:'2rem', textAlign:'center',lineHeight:2.8,marginLeft:'.3rem'},
                          handler: () => messagebox(x.rid, k)
                        }
                      ]">
                        <div class="img" style="margin-left:-3rem;">
                            <img :src="getIcon()" style="width:.9rem;height:.9rem">
                            <i v-if="x.is_readed == 0" ></i>
                        </div>
                        <div class="mess">
                            <h5>{{x.title}}</h5>
                            <p class="p1" v-html='x.content ? x.content.slice(0,21):"错误信息"'></p>
                            <!-- <p class="p1">{{x.content.slice(0,25)+ '...'}}</p> -->
                            <p class="p2">{{formatDateTime(x.date*1000)}}</p>
                        </div>
                    </mt-cell-swipe>
                </li>
                <div class="loading-icon"style="font-size:.35rem;" v-show='icon'><img src="../../assets/img/loading.gif" alt=""></div>
                    <div class="loading-icon" v-show='allLoaded' style="font-size:.35rem;">暂无更多数据</div>
            </ul>
        </mt-loadmore>
        <!-- <div class="warning-box" v-if='!info.length'>暂无任何消息</div> -->
        <navcate></navcate>
    </div>
</template>
<script>
    import Vue from 'vue'
    import units from '../../tools/units'
    import cookie from '../../tools/cookie'
    import navcate from '../template/navcate.vue'
    import { CellSwipe } from 'mint-ui';
    // Vue.component(CellSwipe.name, CellSwipe);

    export default {
        name: 'index',
        data () {
            return {
                content : 'asdas',
                info: [],
                ready:{},
                icon:['img_img1.png','img_img2.png','img_img3.png','img_img4.png'],
                articlePage: 0,
                articleLimit: 10,
                allarticle:'',
                loading:'',
                icon:false,
                complete: false, //数据是否显示完成
                distance:0,
                allLoaded:false,
                topStatus: '',
                noMsg: false, //判断是否有消息
            }
        },
        components: {
            navcate,
            'v-scroll': require("../pull-refresh_message")
        },
        methods: {
            loadTop() {//下拉刷新
                setTimeout(() => {
                  this.getdata(2);
                  this.$refs.loadmore.onTopLoaded();
                }, 500);//延时执行
                // 可以加上刷新完成
            },
            handleTopChange(status) { //下拉刷新状态
                setTimeout(() => {
                }, 500);//延时执行
                this.topStatus = status;
            },
            loadMore(){ //无限加载
			    this.icon = true;
			    setTimeout(() => {
                    this.getdata(1);
                }, 500);//延时执行
            },
            messagebox :function (rid, k) {
                let that = this;
                this.Http('message/deleteMessage',{
                    switch : 'user_delete',
                    rid : rid,
                },function (res) {
                    if(that.info.length == 0) {
                        that.noMsg = true;//判断是否有数据
                    }
                    that.info.splice(k,1)
                }, function () {//请求错误
                    layer.open({
                        content: '服务器响应错误'
                        ,skin: 'msg'
                        ,time: 1 //2秒后自动关闭
                    });
                    return;
                })
            },
            getContent : function (rid, mid, x, k) {
                let that = this;
                if(navigator.onLine==true){  //未联网状态跳转错误页 
                    this.Http('message/content',{
                        rid : rid,
                        mid :mid,
                    },function (res) {
                        layer.open({
                            content: res.info.content
                            ,btn: '关闭'
                            ,style: 'font-size: .4rem;'
                        });
                        that.info[k].is_readed = 1;
                    })
                } else {
                    layer.msg('网络开小差了~~~');
                    return;
                }
            },
            getIcon:function () {
                let that = this;
                return   units.getHost() + '/public/images/rand/img_img1.png'
            },
            formatDateTime: function (str) {
                return units.formatDateTime(str)
            },
            getdata: function (id,ready=0) {
                let that = this;
                if(id == 1){//如果是上拉加载
                    that.articlePage = that.articlePage + that.articleLimit;
                    if((that.articlePage + that.articleLimit) > that.allarticle){
                        this.icon = false;
                        this.loading= true;// 若数据已全部获取完毕
                        this.allLoaded = this.loading;
                    }
                }
                if(id == 2){ //无限加载
                    that.articlePage = 0;
                }
                this.Http('message/listd_page',{
                    ready:ready,
                    switch : 'user',
                    user_id : cookie.get('user_id'),
                    limit:that.articleLimit+that.articlePage,
                },function (res) {
                    if(!res.warning){
                    // if(ready == 0){
                        that.info = res.info;
                        that.allarticle = res.msg;
                        if(res.msg == 0) {
                            that.noMsg = true;//判断是否有数据
                        }
                        localStorage.setItem("messList",JSON.stringify(that.info));
                        if(id == 2){//下拉刷新
                            that.loading = false;
                            
                        }
                        if(id == 3){
                            that.loading = false;//刚刷新进入 不让执行
                        }
                    }
                    else {
                        layer.msg(res.warning)
                    }
                    // }else{
                    //     that.ready = res.info;
                    // }
                })
            }
        },
        created () {
            let that = this;
            if(!units.isLogin()){
                location.href = '#/login';
            }
            if(window.navigator.onLine==true){  //未联网状态跳转错误页  
                this.getdata(3);

                // new Promise(function () {
                //     // that.getdata(1);
                // })
            } else {
                this.info = JSON.parse(localStorage.getItem("messList"))
            }
            this.$store.state.header.leftShow = false
            cookie.set('curr',2);
        },
        beforeCreate: function () {
            units.title.set('我的消息');
        },
        beforeRouteEnter: function (to, from, next) {
            if(!units.isLogin()){
                location.href = '#/login';
            }
            next();
        }
    }
</script>
