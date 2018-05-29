
<template>
    <div id="index"
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
                    <span v-show="topStatus == 'loading'" ><img class="loading-img" src="../assets/img/loading.gif" alt=""></span>
                    <span v-show="topStatus == 'pull'" style="font-size: .3rem;">下拉刷新</span>
                </div>
            <div class="banner"><!-- 轮播图 -->
                <swiper :options="swiperOption" ref="mySwiperA">
                    <swiper-slide v-for="(x, ind) in banner_list" :key='ind' @click.native="DetailBanner(x.url)">
                        <img style="height:5.65rem;" :src='host+x.banner'>
                    </swiper-slide>
                    <div class="swiper-pagination"  slot="pagination"></div>
                </swiper> 
            </div>
            <div class="center">
                <div class="seek" @click="hrefs('findcar')">
                    <img src="../../src/assets/img/icon1.png">
                    <div class="text"><p>寻车</p><p>定位</p></div>
                </div>
                <div class="serve">
                    <ul>
                        <!-- <li @click="hrefs('forum')">
                        <li @click="hrefs('order/list')">
                            <img src="../../src/assets/img/zhixingyew.png">
                            <p>回收业务</p>
                        </li> -->
                        <li @click="hrefs('information')">
                        <!-- <li @click="hrefs('order/list')"> -->
                            <img src="../../src/assets/img/icon2_2.png">
                            <div class="text"><p>业务</p><p>资讯</p></div>
                        </li>
                        <li @click="hrefs('vehicletool')">
                            <img src="../../src/assets/img/zhushoun3.png">
                            <div class="text"><p>车融</p><p>助手</p></div>
                        </li>
                    </ul>
                </div>
            </div>
            
            <div class="article-box">
                <div class="cen_box" v-for="x in article">
                    <div class="lism">
                        <div class="lism_cen clearfix">
                            <a @click="acticleDetails(x.article_id)">
                                <dl>
                                    <dt><img :src="host+x.art_thumb||'/static/img/img_13.28f6603.jpg'"></dt>
                                    <dd>
                                        {{x.art_title}}
                                        <div class="lism_div">
                                            <p class="bianji">编辑：{{x.ad_name}}&nbsp;{{len(x.art_time)}}</p>
                                        </div>

                                    </dd>
                                </dl>
                            </a>

                        </div>
                    </div>
                </div>
                <div class="loading-icon"style="font-size:.35rem;" v-show='icon'><img src="../assets/img/loading.gif" alt=""></div>
                    <div class="loading-icon" v-show='allLoaded' style="font-size:.35rem;">暂无更多数据</div>
                <!-- <div class="fh"></div> -->
            </div>
        </mt-loadmore>
        <navcate></navcate>
    </div>
<!-- f0f4fa -->
    <!--首页-->
</template>
<script>
    import { Loadmore } from 'mint-ui';
    import units from '../tools/units'
    import cookie from '../tools/cookie'
    import navcate from './template/navcate.vue'
    import Vue from 'vue'
    import { swiper, swiperSlide } from 'vue-awesome-swiper'
import { setInterval, clearTimeout } from 'timers';
    Vue.component(Loadmore.name, Loadmore);
    export default {
        name: 'index',
        data () {
            return {
                article: [],
                banner_list:[],
                allarticle:'',
                scrollTop: 0,//滚动的位置
                allLoaded:false,
                moreThat: true,
                host: units.getHost(),
                wrapperHeight:0,
                swiperOption: {
                    autoplay: 5000,
                    // loop: true,
                    pagination: '.swiper-pagination',
                    onSlideChangeEnd: swiper => {},
                    // direction: 'horizontal',
                    grabCursor: true,
                    setWrapperSize: true,
                    paginationClickable: true,
                    autoplayDisableOnInteraction : false,
                    observeParents: true
                },
                articlePage: 0,
                articleLimit: 4, //
                allarticle:'',
                loading:'',
                icon:false,
                complete: false, //数据是否显示完成                
                topStatus: '',
                distance:0,
                info: {}, //获取用户信息
            }
        },
        computed: {
            swiper() {
                return this.$refs.mySwiperA.swiper
            }
        },
        components: {
            navcate,
            swiper,
            swiperSlide,
            'v-scroll': require("./pull-refresh_main")
        },
        methods: {
            loadMore(){
			    this.icon = true;
			    setTimeout(() => {
                    this.getArticle(1);
                }, 500);//延时执行
            },
            handleTopChange(status) { //下拉刷新
                setTimeout(() => {
                }, 500);//延时执行
                this.topStatus = status;
                console.log(status)
            },
            loadTop() {//下拉刷新
                setTimeout(() => {
                  this.getArticle(2);
                  this.$refs.loadmore.onTopLoaded();
                }, 500);//延时执行
                // 可以加上刷新完成
            },
            handleTopChange(status) {
                this.topStatus = status;
            
            },
            hrefs ($url) {
                if(units.isLogin(true)){
                    if(navigator.onLine==true){  //未联网状态跳转错误页 
                        if($url == 'findcar') { //判断是否交押金
                            if( !this.info.enterAuth ) {
                                layer.msg('请先进行资料认证')
                                return false;
                            }
                            this.$http.post(units.host('isDeposit'), units.params()).then(function (res) {
                                if (!res.body.warning) {//
                                    if(res.body.info == 2) {//交押金用户
                                        location.href = '#/'+$url;
                                    } else {
                                        layer.msg(res.body.msg, 1, function () {
                                            location.href='#/depositpay'
                                        })
                                    }
                                } else {
                                    layer.msg(res.body.warning);
                                    return;
                                }
                            }, function () {//请求错误
                                layer.open({
                                    content: '服务器响应错误'
                                    ,skin: 'msg'
                                    ,time: 1 //2秒后自动关闭
                                });
                                return;
                            });
                        } else {
                            location.href = '#/'+$url;
                        }
                    } else {
                        layer.msg('网络开小差了~~~');
                        return;
                    }
                }
            },
            acticleDetails (id) {//点击新闻详情页  
                if(units.isLogin(true)){
                    if(navigator.onLine==true){  //未联网状态跳转错误页 
                        location.href='#/article/content?id='+id
                        this.scrollTop = $("html").scrollTop()
                        console.log(this.scrollTop)
                        cookie.set('scrollTop', $("html").scrollTop())
                    } else {
                        layer.msg('网络开小差了~~~');
                        return;
                    }
                }
            },
            DetailBanner (ind) {
                if(navigator.onLine==true){  //未联网状态跳转错误页 
                    this.$router.push(ind);
                } else {
                    layer.msg('网络开小差了~~~');
                    return;
                }
            },
             
            islogin(){},
            Goto: function (url, login) {
                if (login && !units.isLogin()) {
                    location.href = '/login'
                } else {
                    location.href = url;
                }
            },
            len: function (a) {
                return a.substring(0, 10)
            },
            getArticle(id){
                let that = this;
                let list = [];
                if(id == 1){//如果是上拉加载
                    that.articlePage = that.articlePage + that.articleLimit;
                }

                if(id == 2){
                    that.articlePage = 0;
                }

                this.$http.post(units.host('indexArticle_page'), units.paramsno({
                    page: that.articlePage,
                    limit:that.articleLimit+that.articlePage,
                })).then(function (res) {
                    // console.log(id);
                    // console.log(res.body.msg);
                    that.allarticle = res.body.msg;//总条数
                     that.article = res.body.info;
                    if(id == 1){//如果是上拉加载
                        if((that.articlePage + that.articleLimit) > that.allarticle){
                            this.icon = false;
                            this.loading= true;// 若数据已全部获取完毕
                            this.allLoaded = this.loading;
                        }
                    }
                     if(id == 2){//下拉刷新
                        that.loading = false;
                        
                     }
                     if(id == 3){
                     	that.loading = false;//刚刷新进入 不让执行
                     }
                    that.icon = false;
                     localStorage.setItem("getArticle",JSON.stringify(that.article));

                });
            },
            getdata: function () { //获取用户信息
                this.$http.post(units.host('user_new'), units.params({
                    sw: 'info'
                })).then(function (res) {
                    // console.log(res.data.info.user_anthen)
                    this.info = res.data.info;
                    cookie.set('user_auth', res.data.info.user_anthen)
                    localStorage.setItem("infoData",JSON.stringify(this.info));
                });
            },
            getbanner(){ //获取banner图
                let that = this;
                this.$http.post(units.host('get_banner'), units.paramsno()).then(function (res) {
                    that.banner_list = res.body.info;
                    localStorage.setItem("bannerList",JSON.stringify(that.banner_list));
                });
            }
        },
        activated () {
            this.getdata();
        },
        beforeRouteEnter (to, from, next) {
            var that = this;
            if( from.path == '/article/content'){
                $("html").scrollTop(cookie.get('scrollTop'));
            }else {
                $("html").scrollTop(0)
            }
            next();
        },
        created () {
            let that = this;
            that.articlePage = 0;
            if(window.navigator.onLine==true){  //未联网状态跳转错误页  
                this.getArticle(3);
                this.getbanner();
                this.getdata()

            } else {
                this.banner_list = JSON.parse(localStorage.getItem("bannerList"))
                this.article = JSON.parse(localStorage.getItem("getArticle"))
            }
            /*
                Connection.UNKNOWN	未知连接
                Connection.ETHERNET	以太网连接
                Connection.WIFI	无线网连接
                Connection.CELL_2G	2G网连接
                Connection.CELL_3G	3G网连接
                Connection.CELL_4G	4G网连接
                Connection.CELL	通用连接
                Connection.NONE	无网络连接
            */
            // var networkState = navigator.connection.type;
            // if(networkState){  //未联网状态跳转错误页  
            //     this.getArticle(3);
            //     this.getbanner();
            //     this.getdata()

            // } else {
            //     this.banner_list = JSON.parse(localStorage.getItem("bannerList"))
            //     this.article = JSON.parse(localStorage.getItem("getArticle"))
            // }
            var exitAppTicker = 0;
            document.addEventListener("deviceready",function(){
               // StatusBar.backgroundColorByHexString("#FAB");
                 StatusBar.styleLightContent();
                 /*极光推送*/
                 document.addEventListener("jpush.receiveRegistrationId", function (event) {//首先注册Jpush服务
                        // alert("receiveRegistrationId" + JSON.stringify(event));
                        console.log(event);
                        cookie.set('user_jpushid', event.registrationId);
                  }, false)
                  window.JPush.init();//初始化jpush服务
                  window.JPush.setDebugMode(true);
                    var onOpenNotification = function(event) {
          try {
            var alertContent;
            if (device.platform == "Android") {
              alertContent = event.alert;
            } else {
              alertContent = event.aps.alert;
            }
            alert("open Notification:" + alertContent);
          } catch (exception) {
            console.log("JPushPlugin:onOpenNotification" + exception);
          }
        };
        
        var onReceiveNotification = function(event) {
          try {
            var alertContent;
            if (device.platform == "Android") {
              alertContent = event.alert;
            } else {
              alertContent = event.aps.alert;
            }
            $("#notificationResult").html(alertContent);
          } catch (exception) {
            console.log(exception)
          }
        };
      
        var onReceiveMessage = function(event) {
          try {
            var message;
            if (device.platform == "Android") {
              message = event.message;
            } else {
              message = event.content;
            }
            $("#messageResult").html(message);
          } catch (exception) {
            console.log("JPushPlugin:onReceiveMessage-->" + exception);
          }
        };
      
                  document.addEventListener("jpush.openNotification", onOpenNotification, false);
                  document.addEventListener("jpush.receiveNotification", onReceiveNotification, false);
                  document.addEventListener("jpush.receiveMessage", onReceiveMessage, false);
                /*---安卓返回键----iOS别添加*/
                document.addEventListener("backbutton", function(){
                    var pageUrl = window.location.href;//获取当前页面url
                    var m = pageUrl.lastIndexOf('/');
                    var str = pageUrl.substring(m+1);//截取到最后
                    if(str == '' || str == 'start' || str == 'list' || str == 'index'){//如果是首页点两次推出/????
                        if(exitAppTicker == 0){
                            exitAppTicker++;
                            layer.msg('再点一次退出');
                            setTimeout(function(){
                                exitAppTicker = 0;
                            },2000);
                        }else if(exitAppTicker == 1){
                            navigator.app.exitApp(); //退出app
                        }  
                    }else if(str == 'login' || str == 'findcar'){
                        location.href = '#/';///登陆页点击返回键调到首页
                    }else if(str.indexOf('navigation') != -1){//当寻车付款跳到导航页  不让他返回付款页
                        location.href = '#/server/content?cur=3';
                    }else if(str.indexOf('content') != -1){//当寻车付款跳到导航页 点击返回键 不让他返回付款页 
                        location.href = '#/';
                    }else if(str.indexOf('caremanage') != -1){//当寻车付款跳到导航页  不让他返回付款页
                        location.href = '#/server/start';
                    }else{
                        history.back();//返回上一页
                    }
                }, false);
                /*热更新*/
                chcp.fetchUpdate(function (error, data) {//检查是否有更新并下载
                    // console.log('检查更新')
                    // console.log(data,error);
                    if(!error){
                        layer.open({
                            content: '更新了很多有趣的内容',
                            btn: ['取消', '更新'],
                            shadeClose: false,
                            yes: function(index){
                                chcp.installUpdate(function (error) {//安装更新
                                    if (error) {
                                        layer.msg('安装更新失败');
                                    } else {
                                        layer.msg('安装更新成功');
                                    }
                                });
                            }
                        });
                    }     
                });

            },false);
            // ====================================================================
            this.distance = 0;
            cookie.set('curr',0);
            units.title.set('无维易寻');
                        
        },
    }
</script>

<!--页面css样式-->
<style rel="stylesheet/less" type="text/less" lang="less" scoped>
    //上拉刷新
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
    // 上拉刷新结束
    #index{
        box-sizing: border-box;
    }
    body, html {
        background: #f4f4f4;
    }

    .w90 {
        width: 90%
    }

    .banner {
        width: 100%;
    }

    .banner img {
        width: 100%;
    }

    .center {
        width: 100%;
        background: #fff;
    }

    .center .seek {
        height: 3.05rem;
        border: 1px solid #f1f1f1;
        display: flex;
        justify-content: center;
        align-items: center;
        // line-height: 2.48rem;
    }

    .center .seek img {
        width: 1.4rem;
        height: 1.4rem;
        // float: left;
        // margin-top: 0.6rem;
        // margin-left: 3.5rem;
        margin-right: 0.2rem;
    }

    .center .seek .text {
        font-size: 0.44rem;
        color: #1E1E1E;
        margin-left: .2rem;
        p{
            padding-top: .15rem;
        }
    }

    .serve {
        height: 3.05rem;
        // line-height: 3.05rem;
    }
    .serve ul{
        display: flex;
        height: 100%;
    }
    .serve ul li {
        width: 49.5%;
        height: 100%;
        border-right: 1px solid #f1f1f1;
        display: flex;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 0.44rem;
        color: #1E1E1E;
        .text{
            margin-left: .2rem;
            p{
                padding-top: .15rem;
            }
        }
    }

    .serve ul li img {
        width: 1.4rem;
        height: 1.4rem;
        margin-right: .2rem;
        // margin: 0.8rem 0.4rem 0.8rem 0.8rem;
    }


    .serve ul li:last-child {
        border-right: none;
    }

    .lism {
        background: #fdfdfd;
        margin: 0 0.5rem 0 0.5rem;
        border-bottom: 1px solid #f1f1f1;
        padding: 0.5rem 0;
        &:last-child{
            border:none;
        }
    }

    .img_left {
        float: left;
    }

    .img_left img {
        width: 0.7rem;
        height: 0.7rem;
    }

    .div_left {
        float: left;
        margin-left: 0.4rem;
        margin-top: 0.2rem;
    }

    .div_left p {
        font-size: 0.28rem;
        color: #828282;
    }

    .fiv_right {
        float: right;
        margin-right: 0.3rem;
    }

    .fiv_right img {
        width: 0.36rem;
    }

    .lism_cen {
        margin: 0.1rem 0 0.1rem;
    }

    .lism_cen dl dt {
        width: 23%;
        float: right;
    }

    .lism_cen dl dt img {

        width: 2.2rem;
        height: 1.5rem;
    }

    .lism_cen dl dd {
        width: 70%;
        font-size: 0.38rem;
        color: #282828;
        margin-bottom: 0.3rem;
    }

    .bianji {
        color: #999;
        font-size: 0.4rem;
        float: left;
    }

    .more {
        color: #999;
        font-size: 0.38rem;
        padding: 0.3rem;
        text-align: center;
        background: #f9f9f9;
    }

    .articleBox {
        margin-top: 0.3rem;
        background: #fff;
    }

    .message {
        width: 0.5rem;
        height: 0.5rem;
        float: right;
    }

    .lism_div {
        margin-top: 0.3rem;
    }
    .banner img{
        cursor: pointer;
    }
    .yo-scroll{
        top: 0px !important;
    }
    .cen_box{
        background:#fff;
    }
    .article-box{
        padding-bottom: 1.5rem;
        border-top: .3rem solid #f0f4fa;
    }
   .nullData{
    margin-top: -3rem !important;
   }
   .swiper-container-horizontal > .swiper-scrollbar {
        position: absolute;
        left: 1%;
        bottom: 3px;
        z-index: 50;
        height: 0px;
        width: 0%;
    }

</style>