
<!--页面css样式-->
<style scoped lang='scss'>
    .yo-scroll {
        background: #f0f4fa;
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

    .list {
        width: 90%;
        margin: 0 auto;
        position: relative;
        margin-top: 0.5rem;
        background: #f0f4fa;

    }

    .list ul {
        background: url(../../../src/assets/img/list_bg.png) no-repeat;
        height: 2.9rem;
        width: 100%;
        background-size: 100% 100%;
    }
    .list .ul_list1 {
        background: #fff;
        height: 2.2rem;
        width: 100%;
        background-size: 100% 100%;
        margin-bottom: .3rem;
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
        margin-top: 0.5rem;

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
    }

    a {
        color: blue;
    }

    .find {
        float: left;
        margin-left: 0.6rem;
    }

    .find img {
        margin-top: -0.1rem;
        width: 0.35rem;
        margin-right: 0.2rem;
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
        margin-top: 0.5rem;
        margin-bottom: 0.2rem;
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
    .yzd .ul_list1 {
        background: #fff;
        height: 2.2rem;
        width: 100%;
        background-size: 100% 100%;
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
        right: 0rem;
    }

    .yzd_img img {
        width: 100%;
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
    .yzd_complete{
        right: 3.3rem;
    }
    .yzd_img img {
        width: 100%;
        transform: rotate(-30deg);
        -webkit-transform: rotate(-30deg);    /* for Chrome || Safari */
        -moz-transform: rotate(-30deg);       /* for Firefox */
        -ms-transform: rotate(-30deg);        /* for IE */
        -o-transform: rotate(-30deg);         /* for Opera */
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
    // 看护
    .care-code-mark{
        position: fixed;
        top: 0;
        right: 0;
        left: 0;
        bottom: 0;
        background: rgba(0, 0, 0, .5);
        z-index: 9999;
        text-align: center;
        .care-code-box{
            position: absolute;
            top: 50%;
            margin-top: -40%;
            width: 80%;
            margin-left: 10%;
            border-radius: .2rem;
            height: 7rem;
            background: #fff;
            h4{
                padding-top: .3rem; 
            line-height: 2.3rem; 
            }
            .care-code{
                width: 86%;
                height: 1.3rem;
                line-height: 1.3rem;
                color: #ff5400;
                font-weight: bold;
                margin-left:7%; 
                border: .01rem solid #e1e1e1;
                border-radius: .2rem;
            }
            .careBtn{
                width: 86%;
                height: 1.3rem;
                margin-left:7%; 
                border-radius: .2rem;
                margin-top: 1rem; 
                button{
                    width: 100%;
                    height: 100%;
                    border-radius: .2rem;
                    background: url(../../assets/img/careBtn.png) center no-repeat;
                    background-size: 100% 100%;
                    border:0;
                    outline:none; 
                }
            }
        }
    }
    // 看护结束
    .care-bot{
        display: flex;
        justify-content: space-between;
        position: relative;
    }
    .verification-code{
        position: absolute;
        top:0.13rem;
        right: .8rem;
        background-size: 100% 100%;
        color: #fff;
        font-size: .2rem;
        div{  
            width: 1.8rem;
            border-radius: .08rem;
            font-size: .3rem;
            background: url(../../assets/img/yzmread.png) center no-repeat;
            height: .65rem;
            line-height: .65rem;
        }
    }
    .yo-scroll{
        top: $top +1rem;
    }
    .content{
        padding-top: $top;
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
            <ul class="nav">
                <li :class="{'cur':current[0]}" @click="currentChange(4)"><span>待看护</span></li>
                <li :class="{'cur':current[1]}" @click="currentChange(5)"><span>看护中</span></li>
                <li :class="{'cur':current[2]}" @click="currentChange(6)"><span>交接中</span></li>
                <li :class="{'cur':current[3]}" @click="currentChange(7)"><span>已交接</span></li>
                <li><span class="order" @click="getArticle(orde_id, 'time')">
                        时间
                        <span class="sj-box">
                            <b class="up-sj" :class='{jtActive: !jtFlag}'></b>
                            <b class="down-sj" :class='{jtActive: jtFlag}'></b>
                        </span>
                    </span>
                </li>
            </ul>
            <!-- <div class="yo-scroll"> -->
            <v-scroll ref='aaa' :on-refresh="onRefresh" :on-infinite="onInfinite" :dataList="scrollData">
                <div class="list" >
                    <ul v-if='!current[0] && !current[3] ' v-for="(x,k) in list" class="ul_list">
                        <li  @click="careDetailOrder(x.find_id?x.find_id: 12)"><p class="p1">车牌号码</p>
                            <p>发布时间</p>
                            <p>服务状态</p></li>
                        <li  @click="careDetailOrder(x.find_id?x.find_id: 12)">
                            <p class="must">{{x.card_number}}</p>
                            <p class="must">{{x.nurse_time? len(x.nurse_time): '暂无显示'}}</p>
                            <!-- 状态 4（待看护）、5（看护中）、6（交接中）、7（已完成） -->
                            <p v-if="x.car_status == 4">
                                <a click="href('server/list?sid='+serverType+'&id='+x.find_id)">待看护</a>
                            </p>
                            <p v-if="x.car_status == 5">
                                <a click="href('server/list?sid='+serverType+'&id='+x.find_id)">看护中</a>
                            </p>
                            <p v-if="x.car_status == 6">                      
                                <a click="href('server/list?sid='+serverType+'&id='+x.find_id)">交接中</a>
                            </p>
                            <p v-if="x.car_status == 7">
                                <a click="href('server/list?sid='+serverType+'&id='+x.find_id)">已完成</a>
                            </p>
                        </li>
                        <li class="care-bot" v-if='x.car_status != 4 || x.car_status != 7'>
                            <span class="find"><img src="../../../src/assets/img/care-peo.png">
                                看护人员：{{x.nurse_name? x.nurse_name :'奈落'}}
                            </span>
                            <!-- 大区经理查看验证码 -->
                            <div 
                                class="verification-code" 
                                v-if='(x.car_status == 6) || (x.car_status == 5)'
                                @click="ReadCode(x.find_id)"
                            ><div>交接验证码</div></div>
                            <!-- 大区经理输入验证码 -->
                            <div 
                                class="verification-code" 
                                v-if='(x.car_status == 5 && role =="1"&&platId == "1") ||(x.car_status == 6 && role =="1"&&platId == "1")'
                                @click="inputCode(x.find_id)"
                            ><div>输入验证码</div></div>
                        </li>
                    </ul>
                    <!-- 大区经理看护 -->
                    <ul v-if='current[0] && role =="1"&&platId == "1"' v-for="(x,k) in list" class="ul_list">
                        <li><p class="p1">车牌号码</p>
                            <p>发布时间</p>
                            <p>服务状态</p></li>
                        <li>
                            <p class="must">{{x.card_number}}</p>
                            <p class="must">{{x.nurse_time? len(x.nurse_time): '暂无显示'}}</p>
                            <!-- 状态 4（待看护）、5（看护中）、6（交接中）、7（已完成） -->
                            <p v-if="x.car_status == 4">
                                <a>看护</a>
                            </p>
                        </li>
                        <li class="care-bot" v-if='x.car_status == 4'>
                            <span v-if='false' class="find"><img src="../../../src/assets/img/care-peo.png">
                                看护人员：{{x.nurse_name? x.nurse_name :'奈落'}}
                            </span>
                            <div 
                                class="verification-code"
                                 @click="nurse(x)"
                            ><div>看&nbsp;&nbsp;&nbsp;&nbsp;护</div></div>
                        </li>
                    </ul>
                    <!-- 普通待看护  -->
                    <ul v-if='current[0]&&platId == "0"' v-for="(x,k) in list" class="ul_list1">
                        <li><p class="p1">车牌号码</p>
                            <p>发布时间</p>
                            <p>服务状态</p></li>
                        <li>
                            <p class="must">{{x.card_number}}</p>
                            <p class="must">{{x.nurse_time? len(x.nurse_time): '暂无显示'}}</p>
                            <!-- 状态 4（待看护）、5（看护中）、6（交接中）、7（已完成） -->
                            <p v-if="x.car_status == 4">
                                <a click="href('server/list?sid='+serverType+'&id='+x.find_id)">待看护</a>
                            </p>
                        </li>
                    </ul>   
                    <!-- 已完成 -->
                    <!-- <ul v-if='current[3]' v-for="(x,k) in list" class="ul_list1">
                        <i class="yzd_img"><img src="../../../src/assets/img/section.png"></i>
                        <li><p class="p1">车牌号码</p>
                            <p>发布时间</p></li>
                        <li>
                            <p class="must">{{x.card_number}}</p>
                            <p class="must">{{len(x.card_addtime)}}</p>
                        </li>
                        <li class="care-bot" v-if='x.car_status != 7'>
                            <span class="find"><img src="../../../src/assets/img/care-peo.png">
                                看护人员：{{x.card_city}}
                            </span>
                            <span class="verification-code"><img src="../../../src/assets/img/verification-code.png"></span>
                        </li>
                    </ul> -->
                </div>
                <!-- 已完成 -->
                <div class="yzd " v-if='current[3]'>
                    <ul class="ul_list1" v-for="x in list" @click="careDetailOrder(x.find_id?x.find_id: 12)">  
                        <i class="yzd_img yzd_complete"><img src="../../../src/assets/img/complete.png"></i>
                        <li class="p1"><p>车牌号码</p>
                            <p>发布时间</p>
                        <li class="must">
                            <p>{{x.card_number}}</p>
                            <p>{{x.nurse_time? len(x.nurse_time): '暂无显示'}}</p>
                        </li>
                    </ul>
                </div>
            <!-- </div> -->
            </v-scroll>
                    
            <!--查找中-->
            <div class="loading-wrapper"></div>
        </div>
        <!-- 看护人交接对车码 -->
        <div class="care-code-mark" v-if='readedCode.flag'>
            <div class="care-code-box">
                <h4>看护人交接对车码</h4>
                <div class="care-code">{{readedCode.text}}</div>
                <div class="careBtn" @click="closeReadCode"><button></button></div>
            </div>
        </div>
        <!-- 看护人交接对车码结束 -->
        <!-- 去看护弹窗 -->
        <GoCare 
            v-if='GoCareFlag'
            @goCareFn = 'goCareFn'
            :careData='careData'/>
        <!-- 去看护弹窗 -->
        <!-- 订单详情弹窗 -->
        <careJoining 
            v-show='detailOrderFlag' 
            :detailOrderData = 'detailOrderData'
            @cloCareDet='cloCareDet'/>
        <!-- 订单详情弹窗 -->
        <!-- 交接中输入验证码 -->
            <InputCode 
                v-if='inputCodeFlag' 
                @sureCode = 'sureCode'>
                    <span  v-show='errorWarn'>您输入的验证码匹配不成功</span>
                </InputCode>
        <!-- 交接中输入验证码 -->
    </div>
</template>
<script>
    import units from '@/tools/units'
    import cookie from '@/tools/cookie'
    import headers from '../template/header.vue'
    import GoCare from './components/Gocare'
    import careJoining from './components/CareJoining'
    import InputCode from './components/InputCode'
    export default {
        name: 'index',
        data () {
            return {
                list: [],
                articlePage: 0,
                articleLimit: 6,
                moreThat: true,
                host: units.getHost(),
                current: [true, false, false,false],
                currentNum: 4,
                sid: '',
                search: false,
                status: 1,
                searchKeyword: '',
                show: true,
                count: '',
                timer: null,
                order_by:1,
                jtFlag: false,
                counter: 1, //当前页
                pageStart: 0, // 开始页数
                pageEnd: 0, // 结束页数
                listdata: [], // 下拉更新数据存放数组
                scrollData: {
                    noFlag: false //暂无更多数据显示
                },
                switch: 'user', //是否为大区经理
                role: '0', //大区经理,
                orde_id: '4', //订单默认状态
                GoCareFlag: false, //去看护是否显示
                careData: {
                    card: '1',
                    brand: '2',
                    find_id: '',
                    card_color: ''
                },
                readedCode: {//读取到的验证码
                    flag: false,
                    text: ''
                },
                inputCodeFlag: false, //是否显示输入框弹窗
                each_id: '',//每条订单的id
                detailOrderFlag: false, //订单详情是否显示
                detailOrderData: {},//订单详情数据
                errorWarn: false,//验证码警告提示语
                platId:0, //看护管理类型判断
            }
        },
        components: {
            headers,
            GoCare,
            careJoining,
            InputCode,
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
                }, function () {//请求错误
                    layer.open({
                        content: '服务器响应错误'
                        ,skin: 'msg'
                        ,time: 1 //2秒后自动关闭
                    });
                    return;
                })
            }
        },
        methods: {
            ReadCode (find_id) { //查看验证码
                this.$http.post(units.domin('Nurse/productCode'), units.params({
                    find_id
                })).then(function (res) {
                    if(res.body.code > 0) {
                        this.readedCode.flag = true;
                        this.readedCode.text = res.body.info
                    }
                }, function () {//请求错误
                    layer.open({
                        content: '服务器响应错误'
                        ,skin: 'msg'
                        ,time: 1 //2秒后自动关闭
                    });
                    return;
                });
            },
            nurse (obj) { // 大区经理点击看护（状态）
                this.careData.card = obj.card_number;
                this.careData.brand = obj.card_brand;
                this.careData.find_id = obj.find_id;
                this.careData.card_color = obj.card_color
                this.GoCareFlag = true;
            },
            goCareFn (obj) { //点击去看护
                console.log(obj)
                if(obj.val) {  
                    this.$http.post(units.domin('Nurse/nurseCar'), units.params({
                        nurse_name: obj.info.name,
                        nurse_phone: obj.info.tel,
                        find_id: obj.info.find_id
                    })).then(function (res) {
                        if(res.body.code > 0) {
                            layer.msg(res.body.msg);
                            this.getArticle(4);
                            this.GoCareFlag = false;
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
                } else {
                    this.GoCareFlag = false;
                }
            },
            inputCode (find_id) { //输入验证码
                this.each_id = find_id;
                this.errorWarn = false;
                this.inputCodeFlag = true;
            },
            sureCode (obj) { //确定提交输入的验证码
                console.log(obj)
                if (obj.val) {
                    this.$http.post(units.domin('Nurse/matchCode'), units.paramsno({
                        code: obj.info,
                        find_id: this.each_id
                    })).then(function (res) {
                        console.log(res)
                        if(res.body.code > 0) {
                            layer.msg(res.body.msg);
                            this.getArticle(5);
                            this.errorWarn = false;
                            this.inputCodeFlag = false;
                        } else {
                            this.errorWarn = true;
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
                    this.inputCodeFlag = false;
                }
            },
            closeReadCode () { //关闭查看验证码弹窗
                this.readedCode.flag = false;
            },
            careDetailOrder (find_id) {//点击订单详情
                this.$http.post(units.domin('Nurse/nurseCarDetail'), units.paramsno({
                    find_id
                })).then(function (res) {
                    if(res.body.code > 0) {
                        this.detailOrderData = res.body.info
                        this.detailOrderFlag = true;
                    }
                }, function () {//请求错误
                    layer.open({
                        content: '服务器响应错误'
                        ,skin: 'msg'
                        ,time: 1 //2秒后自动关闭
                    });
                    return;
                });
            },
            cloCareDet () {//关闭订单详情弹窗
                this.detailOrderFlag = false;
            },
            platformCare (id) { //平台看护
                location.href = '#/server/platformCare';
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
                }, function () {//请求错误
                    layer.open({
                        content: '服务器响应错误'
                        ,skin: 'msg'
                        ,time: 1 //2秒后自动关闭
                    });
                    return;
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
                }, function () {//请求错误
                    layer.open({
                        content: '服务器响应错误'
                        ,skin: 'msg'
                        ,time: 1 //2秒后自动关闭
                    });
                    return;
                });
            },
            len: function (str) {
                return str.substring(0, 10);
            },
            currentChange: function (id) {
                this.orde_id = id;
                this.current = [];
                let arr = [4, 5, 6, 7]
                for (let i = 0; i < arr.length; i++) {
                    if (arr[i] == id) {
                        this.current.push(true);
                    } else {
                        this.current.push(false);
                    }
                }
                this.currentNum = id; // 每个阶段的状态
                this.list = [];
                this.articlePage = 0;
                this.moreThat = true;
                
                //if (id == 2) this.status = 2;
                this.status = id+1;
                
                this.getArticle(id);
            },
            onRefresh(done) {
                this.getArticle(this.currentNum, 1);
                // this.getArticle(this.currentNum,1);
                done(); // call done

            },
             onInfinite(done) {
                // console.log(1323);
                this.getArticle(this.currentNum, 2);
                this.counter++;
                let end = this.pageEnd = this.num * this.counter;
                let i = this.pageStart = this.pageEnd - this.num;
                // console.log()
                  let more = this.$el.querySelector('.load-more');
                // let more = this.$el.querySelector('.load-more-main');
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
                            // console.log(111);
                    }
                }
                done();
            },
            noSearch: function () {
                // units.title.set('寻车管理');
                this.search = !this.search
            },
            getArticle(id,type){
                let that = this;
                
                that.scrollData.noFlag = false;
                let order = 'desc';
                if(type == 'time') {   
                        this.jtFlag = !this.jtFlag;
                        if(this.jtFlag) {
                        order = 'asc'
                        } else {
                        order = 'desc'
                        }
                } else if(type == 1){//下拉刷新
                        that.articlePage = 0;
                        this.allLoaded = false;
                }else if(type == 2){
                    
                    let more = this.$el.querySelector('.load-more');
                    that.articlePage = that.articlePage + that.articleLimit;
                    if(that.articlePage + that.articleLimit > that.allarticle){
                        more.style.display = 'none'; //隐藏加载条
                        //走完数据调用方法
                        that.scrollData.noFlag = true;
                    }
                }
                this.$http.post(units.domin('Nurse/nurseList'), units.params({
                    switch: this.switch,
                    status: id,
                    order,
                    limit: that.articleLimit+that.articlePage,
                })).then(function (res) {
                    if(!res.body.warning){
                        this.list = res.body.info.list;
                        that.allarticle = res.body.info.count;//总条数
                    } else {
                        layer.msg(res.body.warning);
                        setTimeout(() => {
                            window.history.go(-1);
                            return;
                        }, 1000)
                    }
                }, function () {//请求错误
                    layer.open({
                        content: '服务器响应错误'
                        ,skin: 'msg'
                        ,time: 1 //2秒后自动关闭
                    });
                    return;
                });
                
            },
            
        },
        beforeCreate: function () {
            this.$store.state.header.open = false;
        },
        created () {
            let that = this;
            this.platId = this.$route.query.type;  //1个人中心大区的看护订单
            if (this.platId == '1') {
                units.title.set('看护订单');
                
                this.$store.state.header.left = function () {
                    location.href = '#/user/index';
                };
                
                //判断是否为大区经理
                if (cookie.get('role') == '1') {
                    this.switch = 'manager';
                    this.role = cookie.get('role');
                } else {    
                    this.switch = 'user'
                }
            } else {//普通人
                units.title.set('看护管理');
                
                this.$store.state.header.left = function () {
                    location.href = '#/server/start';
                };
            }
            this.currentChange (4);
        },
    }
</script>
