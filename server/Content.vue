<!--页面css样式-->
<style scoped lang='scss'>
    .nav {
        width: 100%;
        height: 1rem;
        background: #fff;
    }

    .right {
        float: right !important;
    }
    .nav {
        width: 100%;
        height: 1rem;
        background: #fff;
        display: flex;
        // margin-top:.3rem; 
    }

    .nav li {
        font-size: 0.32rem;
        color: #B4B4B4;
        flex: 1;
        margin-left: 0.4rem;
        margin-right: 0.4rem;
        line-height: 1rem;
        text-align: center;
        border-bottom: .05rem solid #fff;
    }

    .nav li.cur{
        border-bottom: .05rem solid #0c80fe;
        color: #1D1D1D;
        width: 15%;
        margin-left: 0.4rem;
        margin-right: 0.4rem;
    }
    // .nav{
    //     display: flex;
    //     justify-content: space-around;
    //     padding: 0 .3rem;
    // }
    // .nav li {
    //     flex: 1;
    //     font-size: 0.32rem;
    //     color: #B4B4B4;
    //     // width: 15%;
    //     // margin-left: 0.71rem;
    //     // margin-right: 0.71rem;
    //     // float: left;
    //     line-height: 1rem;
    //     text-align: center;
    // }
    // .nav span{
    //     font-size: 0.32rem;
    //     // color: red !important;
    //     padding-top: 0;
    // }


    .list {
        width: 90%;
        margin: 0 auto;
        position: relative;
        margin-top: .7rem;

    }

    .list ul {
        background: url(../../../src/assets/img/list_bg.png) no-repeat;
        height: 2.9rem;
        width: 100%;
        background-size: 100% 100%;
    }

    .list ul li {
        height: 1rem;
        line-height: 0.9rem;
        text-align: center;
        width: 100%;
        /*background: #fff;*/
        color: #1e1e1e;
        font-size: 0.4rem;
    }

    .list ul li p {
        display: inline-block;
        float: left;
        width: 33%;
    }

    .list ul li.must {
        color: #787878;
    }

    .payment {
        width: 90%;
        margin: 0 auto;
        position: relative;
        margin-top: 0.7rem;

    }

    .payment ul {
      background: url(../../../src/assets/img/list_bg.png) no-repeat;
        /*height: 2.9rem;*/
        width: 100%;
        background-size: 100% 100%;
        margin-top: 0.2rem;
        margin-bottom: 0.3rem;
    }

    .payment ul li {
        height: 1rem;
        line-height: 0.9rem;
        text-align: center;
        width: 100%;
        /*background: #fff;*/
        color: #1e1e1e;
        font-size: 0.4rem;
    }

    .payment ul li p {
        display: inline-block;
        float: left;
        width: 33%;
    }

    .payment ul li.must {
        color: #787878;
    }

    .payment ul li a {
        color: #fff;
    }

    .payment .teack {
        color: #0c80fe;
    }

    .con_list ul li p a {
        color: #e65e5e;
    }

    .ul_list {
        margin-bottom: 0.3rem;
        position: relative;
        margin-top: 0.2rem;
        overflow: hidden;
    }

    a {
        color: blue;
    }


    .list ul li a {
        float: right;
        margin-right: 1rem;
        color: #0c80fe;
    }

    .yzd {
        width: 90%;
        margin: 0 auto;
        position: relative;
        margin-top: 0.7rem;

    }

    .yzd ul {
        background: url(../../../src/assets/img/list_bg.png) no-repeat;
        height: 2.9rem;
        width: 100%;
        background-size: 100% 100%;
        margin-top: 0.3rem;
        position: relative;
        overflow: hidden;
    }

    .yzd ul li {
        height: 1rem;
        line-height: 0.9rem;
        text-align: center;
        width: 100%;
        color: #1e1e1e;
        font-size: 0.4rem;
    }

    .yzd ul li p {
        display: inline-block;
        float: left;
        width: 50%;
    }

    .yzd ul li.must {
        color: #787878;
    }

    .yzd div {
        width: 15%;
        background: #73a7fc;
        color: #fff;
        font-size: 0.6rem;
        text-align: center;
        height: 2.9rem;
        float: right;
        writing-mode: vertical-lr;
        padding-left: 0.3rem;
    }

    .yzd ul li a.a1 {
        width: 25%;
        margin-top: -0.09rem;
        float: left;
        display: block;
        margin-left: 0.3rem;
    }

    .yzd ul li a.a2 {
        width: 25%;
        margin-top: -0.09rem;
        float: right;
        display: block;
        margin-right: 0.3rem;
    }

    .yzd ul li a img {
        width: 100%;
    }

    .batten {
        height: 1.25rem;
        line-height: 1.25rem;
        background-color: #3d7fed;
        z-index: 999;
        // font-family: 微软雅黑;
        // font-family: 'Droidsansfallback';
        padding: 0 0.5rem;
        padding-top: 0.24rem;
    }

    .text {
        width: 90%;
        height: 0.8rem;
        line-height: 0.8rem;
        color: #fff;
        font-size: 0.3rem;
        float: left;
        border-radius: 1rem;
        text-indent: 0.3rem;
        background: #5697fe url(../../../src/assets/img/sous.png) no-repeat center left 0.2rem;
        background-size: 7%;
        padding-left: 0.7rem;
    }

    .batten p {
        float: right;
        font-size: 0.3rem;
        color: #fff;
        margin-top: -0.28rem;
    }

    ::-webkit-input-placeholder { /* WebKit browsers */
        color: #fff;
    }

    :-moz-placeholder { /* Mozilla Firefox 4 to 18 */
        color: #fff;
    }

    ::-moz-placeholder { /* Mozilla Firefox 19+ */
        color: #fff;
    }

    :-ms-input-placeholder { /* Internet Explorer 10+ */
        color: #fff;
    }

    .load {
        text-align: center;
        font-size: 0.3rem;
        margin-top: 1rem;
        color: #b4b4b4;
    }

    .yzd_img {
        width: 40%;
        width: 20%;
        display: block;
        position: absolute;
        margin-top: -0.4rem;
        right: 3.3rem;
    }
    .yzd_complete{
        right: 2rem;
    }
    .yzd_img img {
        width: 100%;
        transform: rotate(-30deg);
        -webkit-transform: rotate(-30deg);    /* for Chrome || Safari */
        -moz-transform: rotate(-30deg);       /* for Firefox */
        -ms-transform: rotate(-30deg);        /* for IE */
        -o-transform: rotate(-30deg);         /* for Opera */
    }

    .flat {
        background: url(../../assets/img/img_end.png);
        background-size: 100% 100%;
        font-size: 0.3rem;
        color: #fff;
        width: 2.5rem;
        height: 0.7rem;
        display: block;
        line-height: 0.7rem;
        float: left;
    }

    .yzm_list {
        margin-top: 0.09rem;
        padding: 0 0.3rem;
    }

    .mode {
        background: url(../../assets/img/img_end.png);
        background-size: 100% 100%;
        font-size: 0.3rem;
        color: #fff;
        width: 2.5rem;
        height: 0.7rem;
        display: block;
        line-height: 0.7rem;
        float: right;
    }
  .pay_list{
    margin-top: 0.09rem;
    padding: 0 0.3rem;
  }
  .pay_list a{
    background: url(../../assets/img/img_end.png);
    background-size: 100% 100%;
    font-size: 0.3rem;
    color: #fff;
    width: 3.5rem;
    height: 0.8rem;
    display: block;
    line-height: 0.8rem;
    float: right;
    margin-top: 0.15rem;
  }
  .timer img{
    width: 0.5rem;
    height: 0.5rem;
    float:left;
    margin-top:0.2rem;
  }
  .count{
    margin-left: 0.2rem;
    float:left;
  }
  .sj-box{ 
        position: relative;
        .down-sj{
            font-size: 0;  
            line-height: 0;  
            border-width: .1rem;  
            border-color: #b4b4b4;  
            border-bottom-width: 0;  
            border-style: dashed;  
            border-top-style: solid;  
            border-left-color: transparent;  
            border-right-color: transparent;  
            position: absolute;
            top: .22rem;
            left: .1rem;
        }
        .up-sj{
            font-size: 0;  
            line-height: 0;  
            border-width: .1rem;  
            border-color: #b4b4b4;  
            border-top-width: 0;  
            border-style: dashed;  
            border-bottom-style: solid;  
            border-left-color: transparent;  
            border-right-color: transparent;  
            position: absolute;
            top: .07rem;
            left: .1rem;
        }
    }
    .nav li .sj-box .jtActive{
        border-color: #2c7dfe;
        border-left-color: transparent;
        border-right-color: transparent;
    }
    .wrap{
        overflow-x: hidden;
    }
    .yo-scroll{
        top: 1rem +$top;
    }
    .content{
        padding-top: $top;
    }
    // 再次审核，取消订单按钮
    .find-check-box{
        display: flex;
        justify-content: space-between;
        padding: 0 .6rem;
        margin-top: .08rem;
        .find-check{
            width: 2.2rem;
            height: .75rem;
            line-height: .75rem;
            color: #fff;
            font-size: .4rem;
            span{
                width: 100%;
                display: inline-block;
                background: url('../../../src/assets/img/img_end.png') no-repeat center;
                background-size: 100% 100%;
                border-radius: .02rem;
            }
        } 
    }
</style>
<!--服务详情-->
<template>
    <div class="wrap">
        <headers v-if="search">
            <div class="batten">
                <input class="text" v-model="searchKeyword" type="text" placeholder="请输入车牌关键词进行搜索"/>
                <p @click="noSearch()">取消</p>
            </div>
        </headers>
        <headers v-if="!search"></headers>
        <div class="load" v-if="false">已全部加在完毕</div>
        <div class="content">
            <ul class="nav" v-if="serverType==2">
                <li
                    v-for='(val, ind) in navData' 
                    :key='ind'
                    :class="{'cur':curActiveFlag == ind}" 
                    @click="currentChange( ind,val.status)"
                ><span>{{val.val}}</span></li>
                <!-- <li :class="{'cur':current[0]}" @click="currentChange(-2)"><span>审核中</span></li>
                <li :class="{'cur':current[1]}" @click="currentChange(-1)"><span>未通过</span></li>
                <li :class="{'cur':current[2]}" @click="currentChange(0)"><span>查找中</span></li> -->
                <!-- <li :class="{'cur':current[1]}" @click="currentChange(1)"><span>付款中</span></li> -->
                <!-- <li :class="{'cur':current[3]}" @click="currentChange(2)"><span>已找到</span></li> -->
                <li><span class="order" @click="getArticle(4, 'time')">
                        时间
                        <span class="sj-box">
                            <b class="up-sj" :class='{jtActive: !jtFlag}'></b>
                            <b class="down-sj" :class='{jtActive: jtFlag}'></b>
                        </span>
                    </span>
                </li>
            </ul>
            <v-scroll ref='aaa' :on-refresh="onRefresh" :on-infinite="onInfinite" :dataList="scrollData">
                <!-- listd_page接口 status状态   -1审核中，1查找中,3,已找到,0审核未通过 -->
                <div class="list" v-if="(status == -1&&list[0]) || (status == 0&&list[0]) ||(status == 1&&list[0])">
                    <ul v-for="(x,k) in list" class="ul_list">
                        <i class="yzd_img yzd_complete" v-if='status == 0'><img src="../../../src/assets/img/no-complete.png"></i>
                        <li><p class="p1">车牌号码</p>
                            <p>发布时间</p>
                            <p>车辆状态</p></li>
                        <li>
                            <p class="must">{{x.card_number?x.card_number:'暂无'}}</p>
                            <p class="must">{{x.card_addtime?len(x.card_addtime):'暂无'}}</p>
                            <p v-if="x.find_id">
                                <a click="href('server/list?sid='+serverType+'&id='+x.find_id)">寻车</a>
                            </p>
                            <p v-else>
                                <a click="href('/server/list?sid='+serverType+'&id='+x.nurse_id)">寻车</a>
                            </p>
                        </li>
                        <li class="find-check-box">
                            <span class="find-check" @click="href('findcar?type=1&find_id='+x.find_id)"><span v-if='status == 0'>再次审核</span></span>
                            <span class="find-check" @click="startWarn(x.find_id)"><span>取消订单</span></span>
                        </li>
                    </ul>
                </div>
                <!-- 代付款 -->
                <!-- <div class="payment" v-if="current[1]">
                    <ul class="" v-for="(x,k) in list">
                        <li class="p1"><p>车牌号码</p>
                            <p>发布时间</p>
                            <p>车辆状态</p></li>
                        <li class="must">
                            <p>{{x.card_number}}</p>
                            <p>{{len(x.card_addtime)}}</p>
                            <p class="teack">寻车</p>
                        </li>
                        <li class="pay_list">
                            <span class="timer"><img src="../../../src/assets/img/time.png"></span>
                            <span v-show="show" class="count">{{x.ex_time}}</span>
                            <a @click="href('pay?order='+x.card_order)">去付款</a>

                        </li>
                    </ul>
                </div> -->
                <!--已找到-->
                <div class="yzd " v-if="status == 3">
                    <ul class="" v-for="x in list">  <!--@click.stop="gotorun(x)" -->
                        <i class="yzd_img"><img src="../../../src/assets/img/complete.png"></i>
                        <!--<div @click="href('server/map?id='+x.find_id)">查看车辆</div>-->
                        <li class="p1"><p>车牌号码</p>
                            <p>发布时间</p>
                            <!--<p>车辆状态</p></li>-->
                        <li class="must">
                            <p>{{x.card_number?x.card_number:'暂无'}}</p>
                            <p>{{x.card_addtime?len(x.card_addtime):'暂无'}}</p>
                            <!--<p class="teack">套餐</p>-->
                        </li>
                        <li class="yzm_list">
                            <!-- <a class="flat" @click.stop="goSend(x.find_id)">平台回收</a> -->
                            <!-- <a class="flat" v-if='x.car_status<4 &&role != 1' @click.stop="platformCare(x)">平台看护</a> -->
                            <!-- <a class="mode" @click.stop="href('server/navigation?id='+x.card_number)">查看车辆</a> -->
                            <a class="mode" @click.stop="href('server/navigation?id='+x.card_number+'&find_id='+x.find_id)">查看详情</a>
                            <div v-if="false">
                                <a :class="{right:x.car_status == 3 || x.car_status == 2}" class="a1 flat"
                                   @click.stop="goSend(x.find_id)">
                                    <img src="../../../src/assets/img/but_2.png"></a>
                                <a class="a2 flat" @click.stop="okayOrder(x.find_id)" v-if="x.car_status != 3">
                                    <img src="../../../src/assets/img/queren.png">
                                </a>
                            </div>
                        </li>
                    </ul>
                </div>
            </v-scroll>
                    
            <!--查找中-->
            <div class="loading-wrapper"></div>
        </div>

        <!-- 取消订单弹框提示 -->
        <WarnAlert 
            v-if='warnFlag'
            @close='closeWarn'/>
    </div>
</template>
<script>
    import units from '@/tools/units'
    import cookie from '@/tools/cookie'
    import headers from '../template/header.vue'
    import WarnAlert from '@/components/frame/warnAlert.vue'
    export default {
        name: 'index',
        data () {
            return {
                serverType: 1,
                list: [],
                articlePage: 0,
                articleLimit: 5,
                moreThat: true,
                host: units.getHost(),
                curActiveFlag:0,//tab类名
                navData: [
                    // {
                    //     val:'审核中',
                    //     status: -2,
                    // },
                    // {
                    //     val:'未通过',
                    //     status: -1,
                    // },
                    // {
                    //     val:'查找中',
                    //     status: 0,
                    // },
                    // {
                    //     val:'已找到',
                    //     status: 2,
                    // }
                ],
                currentNum: 0,
                sid: '',
                search: false,
                status: 1,
                searchKeyword: '',
                show: true,
                count: '',
                timer: null,
                order_by:1,
                role: '1', //是否为大区经理
                jtFlag: false,
                counter: 1, //当前页
                num: 2, // 一页显示多少条
                pageStart: 0, // 开始页数
                pageEnd: 0, // 结束页数
                listdata: [], // 下拉更新数据存放数组
                scrollData: {
                    noFlag: false //暂无更多数据显示
                },
                warnFlag: false, //取消订单的开关
                find_id: 0, //点击取消订单的每一条对应的订单号
            }
        },
        components: {
            headers,
            WarnAlert,
            'v-scroll': require("../pull-refresh")
        },
        watch: {
            'searchKeyword': function () {
                let that = this;
                that.list = [];
                this.Http('find/search', {
                    status: that.status,
                    keyword: that.searchKeyword,
                    type: that.currentNum
                }, function (res) {
                    that.list = res.info;
                    
                    that.moreThat = false;
                })
            }
        },
        methods: {
            startWarn (find_id) {//点击取消订单按钮
                this.find_id = find_id;
                this.warnFlag = !this.warnFlag;
            },
            closeWarn (id) {//关闭取消提示弹框 
                if(id) {
                    this.$http.post(units.domin('find/cancleFindCard'), units.params({
                        find_id: this.find_id
                    })).then(function (res) {
                            console.log(res)
                        if(res.body.code > 0) {
                            layer.msg(res.body.msg);
                        } else {
                            layer.msg(res.body.msg);
                        }
                    }, function () {//请求错误
                        layer.open({
                            content: '服务器响应错误'
                            ,skin: 'msg'
                            ,time: 1 //2秒后自动关闭
                        });
                        return;
                    });
                }
                this.getArticle(2,0);
                this.warnFlag = !this.warnFlag;
            },
            platformCare (obj) { //平台看护
                console.log(obj)
                location.href = '#/server/platformCare?data='+JSON.stringify(obj);
            },
            gotorun:function (x) {
                location.href = '#/server/details?cid='+x.find_id;
            },
            okayOrder: function (id) {
                this.Http('find/okayFind', {
                    id: id,
                    status: 3
                }, function (res) {
                    layer.msg(res.msg, 3, function () {
                        if (res.code > 0) {
                        }
                    })
                })
            },
            goSend: function (id) {
                let that = this;
                this.Http('order/Isterrace', {
                    id: id
                }, function (res) {
                    if (res.info[0]) {
                        layer.open({
                            content: '您已经发布过此寻车订单了',
                            btn: ['查看订单', '我知道了'],
                            shadeClose: false,
                            yes: function () {
                                layer.closeAll();
                            },
                            no: function () {
                                that.href('order/details?id=' + res.info[0].ex_oid);
                            }
                        });
                    } else {
                        that.href('server/terrace?id=' + id+'&carId='+res.info[1])
                    }
                });
            },
             onRefresh(done) {//下拉刷新
                this.getArticle(this.currentNum,1);
                done(); // call done

            },
             onInfinite(done) {//上拉加载
             	this.getArticle(this.currentNum,2);
                this.counter++;
                let end = this.pageEnd = this.num * this.counter;
                let i = this.pageStart = this.pageEnd - this.num;
                let more = this.$el.querySelector('.load-more');
                for(i; i < end; i++) {
                    if(i >= 30) {
                        more.style.display = 'none'; //隐藏加载条
                        //走完数据调用方法
                        this.scrollData.noFlag = true;
                        break;
                    } else {
                        this.listdata.push({
                            date: "2017-06-1"+i,
                            portfolio: "1.5195"+i,
                            drop: i+"+.00 %" ,
                            state: 2
                        })
                        more.style.display = 'none'; //隐藏加载条
                    }
                }
                done();
            },
            len: function (str) {
                return str.substring(0, 10);
            },
            currentChange (ind, id) {
                this.curActiveFlag = ind;
                this.currentNum = id; 
                this.list = [];
                this.articlePage = 0;
                this.moreThat = true;
                
                //if (id == 2) this.status = 2;
                this.status = id+1; //寻车每个状态
                
                this.getArticle(id);
            },
            timeer: function (time) {
                return units.timemake(time)
            },
            moreThatText: function () {
                return this.moreThat == true ? '查看更多' : '全部加载完成';
            },
            noSearch: function () {
                units.title.set('寻车管理');
                this.search = !this.search
            },
            getPayOrder(){
                
            },
           getArticle(id,type){
            //    id 值为4的时候，时间排序，目前别的值没有什么作用
               if(type == 'time') {   
                    this.jtFlag = !this.jtFlag
               }
                let that = this;
                that.scrollData.noFlag = false;
                let $url = 'find/listd_page';
                // let more = that.$el.querySelector('.load-more')
                
                if(id == 4){ //时间排序
                    // if(this.order_by == 1){
                    //     this.order_by = 2;
                    //     // that.articlePage
                    // }else{
                    //     this.order_by = 1;
                    // }
                    that.list.reverse();
                    return;
                }else{
                     this.order_by = 1;
                }
                id = this.currentNum;
                if (id == 1) {
                    $url = 'order/status_page';
                    that.status = 1;
                }
                if(type == 1){//下拉刷新
                    that.articlePage = 0;
                    this.allLoaded = false;
                }else if(type == 2){
                     that.articlePage = that.articlePage + that.articleLimit;
                    if(that.articlePage + that.articleLimit > that.allarticle){
                        // more.style.display = 'none'; //隐藏加载条
                        //走完数据调用方法
                        that.scrollData.noFlag = true;
                    }
                }
                
                this.Http($url, units.paramsno({
                    page: that.articlePage,
                    limit: that.articleLimit+that.articlePage,
                    status: that.status,
                    order_by:that.order_by,
                }), function (res) {
                    if(!res.warning){
                        that.list = res.info;
                        let list = that.list;
                        
                        that.allarticle = res.msg;
                        // for (let x in list) {
                            
                        //     // 当前时间戳
                        //     // 下单距离1小时还剩时间（分钟）
                        //     if ( id == 1) {
                        //         var set_id = setInterval(function(){
                        //             var d = list[x]['card_addtime']; 
                        //             var temp = Date.parse(d.replace(/-/g,"/"));
                        //             var f = new Date();
                        //                 var youWant1=f.getFullYear() + '-' + (f.getMonth() + 1) + '-' + f.getDate() + ' ' + f.getHours() + ':' + f.getMinutes() + ':' + f.getSeconds(); 
                        //             let timestamp = Date.parse(youWant1.replace(/-/g,"/"));
                        //             let ex_time_s = (3600 - (timestamp-temp)/1000)%60;
                        //             let ex_time_m = Math.floor((3600 - (timestamp-temp)/1000)/60)-3;
                        //             if(ex_time_s < 10 && ex_time_s >= 0){
                        //                 ex_time_s = '0' + ex_time_s;
                        //             }
                        //             if(ex_time_m < 10 && ex_time_m >= 0){
                        //                 ex_time_m = '0' + ex_time_m;
                        //             }
                        //             let ex_time = ex_time_m + ':' + ex_time_s;
                        //             if(ex_time_s <= 0 && ex_time_m <= 0){
                        //                 that.Http('find/listd_delete', {
                        //                     order_no: list[x]['card_order'],
                        //                 }, function (res) {
                        //                     if(res.info == '订单已删除'){
                        //                     that.list.splice(x,1);
                        //                 }
                        //                 });
                        //                 clearInterval(set_id);
                        //                 return false;
                        //             }
                        //                 that.$set(list[x],'ex_time',ex_time);
                        //         },1000);//一分钟一次
                        //     }
                        // }
                    } else {
                        layer.msg(res.warning);
                        setTimeout(() => {
                            window.history.go(-1);
                            return;
                        }, 1000)
                    }
                });
            },
            getTabData () {//寻车tab数据
                this.$http.post(units.domin('banner/getFindcarBanner'), units.params()).then(function (res) {
                    this.navData = eval("("+res.data.info+")");
                    let curs = parseInt(this.$route.query.cur);
                    if(curs){
                        this.currentChange(this.navData.length-1,this.navData[this.navData.length-1].status);
                    }else{
                        this.status = this.navData[0].status+1;
                        this.getArticle(2,0);
                    }
                }, function () {//请求错误
                    layer.open({
                        content: '服务器响应错误'
                        ,skin: 'msg'
                        ,time: 1 //2秒后自动关闭
                    });
                    return;
                });
            }
        },
        beforeCreate: function () {
            this.$store.state.header.open = false;
        },
        created: function () {
            let that = this;
            units.title.set('寻车管理');
            this.getTabData ();
            this.role = cookie.get('role');
            this.serverType = 2;
            this.$store.state.header.right = false;
            this.$store.state.header.rightTouch = function () {
                that.noSearch();
            };
            this.$store.state.header.left = function () {
                location.href = '#/server/start';
            };
            var pageUrl = window.location.href;//获取当前页面url
                    var m = pageUrl.lastIndexOf('/');
                    var str = pageUrl.substring(m+1);//截取到最后
                    console.log(str);
            
        },
        mounted: function () {
        }
    }
</script>
