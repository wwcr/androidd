<!--页面css样式-->
<style scoped lang='scss'>
    .resg {
        background: #f2f6f7;
        font-size: 0.4rem;
        // padding: 0.2rem 0.38rem 0.5rem .38rem; 
    }

    .in_list {
        background: #fff;
        border-top: 1px solid #f1f1f1;
        margin-top: .3rem;
        border-bottom: 1px solid #f1f1f1;
        /*margin-bottom: 0.3rem;*/
    }

    .in_list li {
        height: 1.49rem;
        border-bottom: 1px solid #f1f1f1;
        overflow: hidden;
        margin-left: 0.4rem;
    }

    .in_list li a {
        display: block;
        position: relative;
        padding-right: 0.47rem;
        height: 1.49rem;
        line-height: 1.49rem;
        min-height: 1.49rem;
    }

    .in_list li a label {
        font-size: 0.48rem;
        color: #1e1e1e;
    }

    .in_list li a label img {
        width: 0.65rem;
        height: 0.65rem;
        vertical-align: middle;
        margin-top: -0.05rem;
        margin-right: 0.33rem;
    }

    .in_list .message {
        position: relative;
        float: right;
        margin: 0;
        height: auto;
        width: 70%;
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
        color: #d3d5dc;
        font-size: 0.48rem;
        line-height: 1.48rem;
        display: inline-block;

    }

    .in_list .message input {
        border: none;
        background: none;
        font-size: 0.48rem;
        color: #1e1e1e;
        margin-top: 0.05rem;
        -webkit-tap-highlight-color: transparent;
        /* font-family: "微软雅黑"; */
        /* font-family: 'Droidsansfallback'; */
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
        width: 100%;
    }

    .mess {
        float: right;
        width: 60%;
        height: 100%;
        padding-top: 0.5rem;
    }

    .mess_mess {
        width: 10%;
    }

    .mess img {
        width: 0.36rem;
        height: 0.36rem;
        float: right;
    }

    .cur img {
        width: 0.36rem;
        height: 0.36rem;
    }

    .in_list li a.list {
        font-size: 0.48rem;
        color: #1e1e1e;
    }

    .in_list li a.list .text {
        width: 2rem;
        height: 0.9rem;
        border: 1px solid #f1f1f1;
        margin-right: 0.3rem;
        margin-top: 0.3rem;
        text-indent: 0.2rem;
    }

    .location {
        background: #fff;
    }

    .location ul li {
        height: 2rem;
        /*border-bottom: 1px solid #f1f1f1;*/
        overflow: hidden;
        margin-left: 0.4rem;
        line-height: 1.5rem;
    }

    .location ul li a {
        display: block;
        // position: relative;
        padding-right: 0.47rem;
        padding-top:.15rem; 
    }

    .location ul li a p {
        font-size: 0.48rem;
        color: #1e1e1e;
        width: 80%;
        display: inline-block;
        line-height: .8rem;
    }

    .location ul li a p span {
        display: block;
        /*margin-left: 0.4rem;*/
    }

    .location ul li a p span i {
        color: #f05c27;
        font-weight: 600;
        font-style: normal;
        margin-left: 0.1rem;
    }

    .loca {
        float: right;
        margin-top: 0.5rem;
    }

    .loca img {
        width: 0.36rem;
        height: 0.36rem;
        float: right;
    }
    
    .sub_btn{
        background: #f0f4fa;
        margin-top: .2rem;
    }
    .pay{
        height: 100%;
        background: #f0f4fa;
        padding-top: $top; /* 头部Header  paddingTop*/
    }
 /* 协议入口开始 */
    .agreement-warn{
        padding: .5rem;
        font-size: .4rem;
        box-sizing: border-box;
        .agreement-entry{
            color: #2c7dfe;
        }
    }
    .check-con{
        label{
            margin-left:.25rem;
        }
    }
    .check-con {  
    // width: 25px;  
    // margin: 20px 100px;  
        position: relative;  
        left: -.05rem;
        margin-right: .3rem;
    }  
    .check-con input[type=checkbox] {  
        visibility: hidden;  
        width: .4rem;
        height: .4rem;
        position: relative; 
        top: .1rem;
        left: -.03rem;
    }  
    .check-con label {  
        cursor: pointer;  
        position: absolute;  
        width: .5rem;  
        height: .5rem;  
        top: .0rem;  
        left: -0.3rem;  
        background: #fff;  
        border:.02rem solid #bfc2c6;  
        -moz-border-radius: 50%;      /* Gecko browsers */  
        -webkit-border-radius: 50%;   /* Webkit browsers */  
        border-radius:50%;            /* W3C syntax */  
    }  
    .check-con label:after {  
        opacity: 0;  
        content: '\2713';  
        font-size: .35rem;
        text-align: center;
        position: absolute;  
        width: .5rem;  
        height: .5rem; 
        line-height: .5rem;
        border-radius:50%;      
        background: #2c7dfe;
        color: #fff;
        top: -0.015rem;  
        left: -.01rem; 
    } 
    .check-con input[type=checkbox]:checked + label:after {  
        opacity: 1;
    }  
/* 协议入口结束 */
</style>
<template>
    <!--委托寻车押金页面-->
    <div class="pay">
        <div class="resg" v-if="!model" style="padding-top: .5rem;">
             <!-- 您已经成功填写需要看护车辆的详细资料，请完成付款，正式启动该服务！  -->
        </div>
        <!-- <div class="resg" v-if="model" style="padding-top: 1.5rem;">
            请选择寻车服务内容，完成付款开始该服务。
        </div> -->
        <div class="in_list" v-if="false">
            <ul>
                <li v-for="(x,k) in getServerData">
                    <a>
                        <label>{{k+1}}.{{x.service_text}}</label>
                        <span class=" mess mess_mess" @click="serverClick(k,x)">
                            <img src="../assets/img/img_18.jpg" v-if="!serverChose[k]">
                            <img src="../assets/img/cur.jpg" v-else>
                        </span>
                    </a>
                </li>
                <li>
                    <a class="list">
                        价格：<input type="text" v-model="price" class="text" readonly>元
                    </a>
                </li>
            </ul>
        </div>
        <div class="location">
            <ul>
                <li @click="serverClick(0)">
                    <a>
                        <p>交押金后方可使用寻车服务<span>服务价格：<i>¥{{price}}</i></span></p>
                        <!--<span class="loca">-->
                          <!--<img src="../assets/img/img_18.jpg" v-if="!serverChose[0]">-->
                          <!--<img src="../assets/img/cur.jpg" v-else>-->
                        <!--</span>-->
                    </a>
                </li>
                <li @click="serverClick(1)" v-if="false">
                    <a>
                        <p>1. 获得车辆位置，手机报警发送位置<span>服务价格：¥<i>300</i></span></p>
                        <span class="loca">
                          <img src="../../assets/img/img_18.jpg" v-if="!serverChose[1]">
                          <img src="../assets/img/cur.jpg" v-else>
                        </span>
                    </a>
                </li>
            </ul>
        </div>
        <div class="in_list">
            <ul >
                <li>
                    <a>
                        <label><img src="../../assets/img/img_15.png">微信支付</label>
                        <span class="arrow_right"></span>
                        <span class="mess" @click="CpClick(0)">
                            <!-- <img src="../assets/img/img_18.jpg" v-if="!choseImg[0]"> -->
                            <!-- <img src="../assets/img/cur.jpg" v-else> -->
                        </span>
                    </a>
                </li>
            </ul>
        </div>
        <div class="agreement-warn">
            <span class="check-con">
                <input type="checkbox"  value="1" id="checkbox1" >
                <label for="checkbox1"></label>
            </span>
            <span class="agreement-marked">阅读后请您同意<span class="agreement-entry" @click="href('depositcontent?price='+price)">《委托寻车押金协议》</span></span>
        </div>

        <!-- <tips v-if="tips">
            <div class="fixed-ad-img">
                <img src="../assets/img/order.png">
                <div class="point">
                    <a class="look" @click="href('order/list')">
                        <img src="../assets/img/order_1.png">
                    </a>
                    <a class="goon" @click="href('server/content?sid=2')">
                        <img src="../assets/img/order_2.png">
                    </a>
                </div>
                <div class="close-fixed-ad" @click="goIndex()"></div>
            </div>
        </tips> -->

        <div class="sub_btn">
            <a @click="submit">立即支付</a>
        </div>
    </div>
</template>
<script src="//wx.gtimg.com/wxpay_h5/fingerprint2.min.1.4.1.js"></script>
<script>
    import units from '@/tools/units'
    import cookie from '@/tools/cookie'
    export default {
        name: 'index',
        data () {
            return {
                chose: false,
                choseImg: [true, false, false],
                currentId: '',
                model: true,
                // tips:false,
                price: 2800,
                serverChose: [true, false],
                servernum: '1',
                set_id: null, //一分钟支付一次订单定时器
                getServerData: {}
            }
        },
        methods: {
             goIndex(){
                this.tips = !this.tips;
                location.href = '#/';
            },
            serverClick: function (id) {
                this.serverChose = [];
                for (let i = 0; i < 2; i++) {
                    this.serverChose.push(false);
                }
                this.serverChose[id] = true;
            },
            CpClick: function (id) {
                this.curInit();
                this.choseImg[id] = true;
                this.currentId = id;
            },
            curInit: function () {
                this.choseImg = [];
                for (let i = 0; i < 3; i++) {
                    this.choseImg.push(false);
                }
            },
            getServer: function () {
                this.$http.post(units.host('server'), units.params({
                    type: this.$route.query.type,
                    sw: 'get'
                })).then(function (res) {
                    this.getServerData = res.data.info;
                });
            },
            submit: function () {
                let that = this;
                let order = this.$route.query.order;
                if (this.model) {
                    if (parseInt(that.price) <= 0 || !parseInt(that.price)) {
                        layer.msg('订单价格不能少于0元');
                        return false;
                    }
                    if (!that.servernum) {
                        layer.msg('请选择一种服务');
                        return false;
                    }
                }
                if(!$("input[type='checkbox']").is(':checked')) {
                    layer.msg('请阅读委托押金协议');
                    return;
                }
                layer.loading('请稍等...');
                console.log(that.price)
                // this.$http.post(units.domin('pay/wechat_pay'), units.params({
                    this.$http.post(units.domin('pay/wechat_pay_new'), units.params({
                    type: that.currentId,
                    user_id: cookie.get('user_id'),
                    switch: 'deposit',
                    price: that.price,
                    serviceType: cookie.get('serviceType'),//那种服务区分,
                    server: that.servernum,//如果有服务类别,用户勾选的服务
                })).then(function (res) {
                    layer.loading(false);
                    // console.log(res.data.mweb_url);
                     // window.location.href = res.data.mweb_url; //ios支付
                    // //  android app支付  -->wy
                    var params = {
                        partnerid: res.body.partnerid, // merchant id
                        prepayid: res.body.prepayid, // prepay id
                        noncestr: res.body.noncestr, // nonce
                        timestamp: res.body.timestamp, // timestamp
                        sign: res.body.sign, // signed string
                    };

                    Wechat.sendPaymentRequest(params, function () {
                        // layer.loading('请稍等...');
                        that.$http.post(units.domin('Nurse/paystatus'), units.params({
                            switch: 'deposit'
                        })).then(function (res) {
                            if(res.body.code == 2){
                                location.href= '#/Findcar';
                                return false;
                            }//该订单已支付
                        });
                    }, function (reason) {
                        
                    });
                });
            },
            timerFn () {
                let that = this;
                // that.set_id = setInterval(function(){
                //     that.$http.post(units.domin('Nurse/paystatus'), {
                //         user_id: cookie.get('user_id'),
                //         switch: 'deposit'
                //     }).then(function (res) {
                //         if(res.body.code == 2){//该订单已支付
                //             clearInterval(that.set_id);
                //             location.href= '#/Findcar';
                //             return false;
                //         } else if(res.body.code == 0) {
                //             layer.msg(res.body.msg)
                //         }
                            
                //     });
                // },1000);//       

            },
            priceShow () {
                this.$http.post(units.host('get_sale', 'api'), units.paramsno({
                    type: 3,//1==》寻车定位 2==》看护  3==>押金
                })).then( function (res) {
                    this.price = res.body.info[0].current_money;
                    this.priceInfo = res.body.info[0];
                })
            }
        },
        mounted(){   
            this.timerFn();
            // console.log('mounted')
        },
        destroyed () {
            clearInterval(this.set_id);
            // console.log('destroyed')
        },
        deactivated () {
            clearInterval(this.set_id);
            // console.log('deactivated')
        },
        activated () {
            units.title.set('委托寻车押金');
            this.priceShow();
            // this.timerFn();
            // console.log('activated')  
            // clearInterval(this.set_id);
        },
        created: function () {
            this.curInit();
            this.CpClick(0);
            units.title.set('委托寻车押金');
            this.priceShow();
            if (this.$route.query.type == 2) {
                this.model = true;
                this.getServer();
            } else {
                this.model = false;
            }
            this.$store.state.header.left = function () {
                location.href = '#/';
            };
        },
        components: {
            // tips
        }
    }
    
</script>
