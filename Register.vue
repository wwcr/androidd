<!--页面css样式-->
<style scoped lang='scss'>
    .logo {
        width: 100%;
        padding-top:$top; 
    }

    .logo img {
        width: 100%;
    }

    .pass {
        padding: 0.1rem 1.3rem;
        background: #fff;
    }

    .pass_inp {
        height: 1.5rem;
        line-height: 1.3rem;
        border-bottom: 1px solid #f1f1f1;
        margin-bottom: 0.5rem;
    }

    .pass_inp input {
        border: none;
        width: 90%;
        overflow: hidden;
        font-size: 0.4rem;
        text-indent: 0.2rem;
        /*
                height: 0.7rem;
                padding: 0.6rem 0;*/
    }

    .pass_inp input.text_a {
        // width: 40% !important;
    }

    .huoqu {
        float: right;
        /*width: 40%;*/
        height: 1rem;
        line-height: 1rem;
        text-align: center;
        /*border:1px solid #3d7fed;*/
        color: #3d7fed;
        border-radius: 38px;
        font-size: 0.4rem;
        margin-top: 0.2rem;
    }

    .company {
        color: #999;
        font-size: 0.32rem;
        // position: absolute;
        // bottom: 3%;
        // margin-left: 23%;
        margin-top: 1rem;
        height: 1rem;
    }

    .company a {
        color: #0c80fe;
    }

    .eye {
        background: url(../../src/assets/img/open.png) no-repeat;
        background-size: 100% 100%;
        position: absolute;
        right: 0;
        top: 40%;
        width: 0.6rem;
        height: 0.32rem;
    }
    .close{
        background: url(../../src/assets/img/close.png) no-repeat;
        background-size: 100% 100%;
        position: absolute;
        right: 0;
        top: 40%;
        width: 0.6rem;
        height: 0.32rem;
    }
    .po_reg {
        position: relative;
    }

    .dianji a {
        color: #377bee;
        font-size: 0.38rem;
        margin-top: .3rem;
    }

    .dianji .dian_l {
        float: left;
    }

    .dianji .dian_r {
        float: right;
    }

    .submint {
        background: #a3a3a3;
    }
    /* 单选框 */
    .check-con{
        position: absolute;
        top: -0.05rem;
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
        // line-height: .5rem;
        border-radius:50%;      
        background: #2c7dfe;
        color: #fff;
        top: -0.015rem;  
        left: -.01rem; 
    } 
    .check-con input[type=checkbox]:checked + label:after {  
        opacity: 1;
    }  
    #Register{
        background: #fff;
        height: 100%;
    }


    .inp {
            border: 1px solid gray;
            padding: 0 10px;
            width: 200px;
            height: 30px;
            font-size: 18px;
        }
        .btn {
            border: 1px solid gray;
            width: 100px;
            height: 30px;
            font-size: 18px;
            cursor: pointer;
        }
        #embed-captcha {
            width: 300px;
            margin: 0 auto;
        }
        .show {
            display: block;
        }
        .hide {
            display: none;
        }
        #notice {
            color: red;
        }
</style>
<template>
    <div id="Register">
        <div class="logo">
            <img src="../assets/img/logo.jpg">
        </div>
        <!-- 忘记密码start -->
        <div class="pass" v-if="form.type==1">
            <div class="pass_inp">
                <input type="tel" v-model="form.user_mobile" @input= 'getYzmVal' class="text" placeholder="请输入手机号" @click="fsl">
            </div>

            <div v-if='isYzmFlag'>
            <!-- 极验start -->
                <div id="embed-captcha"></div>
                <p id="wait" class="show">正在加载验证码......</p>
                <p id="notice" class="hide">请先完成验证</p>
            <!-- 极验end -->
            
            </div>
            <div class="pass_inp" v-if='isInputPwd'>
                <!-- <input type="tel" v-model="form.qcode" class="text_a" placeholder="获取短信验证码">
                <a class="huoqu" @click="sendQcode">{{changeText}}</a> -->
                <input type="tel" v-model="form.qcode" class="text_a" placeholder="获取短信验证码" @click="fsl">
                <!-- <a class="huoqu" v-if='codeFlag' @click="sendQcode">{{changeText}}</a>
                <a class="huoqu" v-if='!codeFlag'>{{changeNumber}}秒后重新获取</a> -->
            </div>
            <div class="pass_inp" v-if='isInputPwd'>
                <input type="password" v-model="form.user_password" class="text" placeholder="请输入8-16位英文字母/数字/符号" @click="fsl">
            </div>
            <div class="sub_next" v-if='isInputPwd'>
                <a class="" @click="next">找回密码</a>
            </div>
        </div>
        <!-- 忘记密码end -->
        <!-- 注册start -->
        <div class="pass" v-else>
            <!--<div class="pass_inp">-->
            <!--<input type="text" v-model="form.user_username" class="text" placeholder="请填写昵称">-->
            <!--</div>-->

            <div class="pass_inp">
                <input type="tel" v-model="form.user_mobile" @input= 'getYzmVal' class="text" placeholder="请输入手机号" @click="fsl">
            </div>
            
            <div v-if='isYzmFlag'>
            <!-- 极验start -->
                <div id="embed-captcha"></div>
                <p id="wait" class="show">正在加载验证码......</p>
                <p id="notice" class="hide">请先完成验证</p>
            <!-- 极验end -->
            
            </div>
            <div class="pass_inp" v-if='isInputPwd'>
                <input type="tel"  v-model="form.qcode" class="text_a" placeholder="请输入短信验证码" @click="fsl">
                <!-- <a class="huoqu" v-if='codeFlag' @click="sendQcode">{{changeText}}</a>
                <a class="huoqu" v-if='!codeFlag'>{{changeNumber}}秒后重新获取</a> -->
            </div>
            <div class="pass_inp po_reg" v-if='isInputPwd'>
                <input v-if="eys_close" type="text" v-model="form.user_password" class="text"
                       placeholder="请输入8-16位英文字母/数字/符号" @click="fsl">
                <input v-if="!eys_close" type="password" v-model="form.user_password" class="text"
                       placeholder="请输入8-16位英文字母/数字/符号" @click="fsl">
                <div class='eye' :class="{close:!eys_close}" @click="eye_click"></div>
            </div>
            <div class="dianji">
                <a href="#/" class="dian_l">返回首页</a>
                <a href="#/login" class="dian_r">已有账户登陆</a>
            </div>
            <div class="sub_next" v-if='isInputPwd'>
                <a @click="next">注册</a>
            </div>
            <div class="company" v-if='isInputPwd'>
                <span class="check-con">
                    <input type="checkbox"  value="1" id="checkbox1" >
                    <label for="checkbox1"></label>
                </span>
                我已阅读并同意<a @click="hrefArgeementPage()">《软件使用协议》</a>
            </div>
        </div>
        <!-- 注册end -->
        <UserAgreement v-if='argeementFlag'/>
    </div>
    <!--注册,忘记秒密码-->
</template>
<script src="http://static.geetest.com/static/tools/gt.js"></script>
<script>
    import units from '../tools/units'
    import cookie from '../tools/cookie'
    import UserAgreement from '@/components/find/agreement'
    // import md5 from 'js-md5'
    import gt from '../../static/gt.js'
    export default {
        name: 'index',
        data () {
            return {
                form: {
                    user_username: '用户',
                    user_mobile: '',
                    qcode: '',
                    user_password: '',
                    type: '',
                },
                changeNumber: 60,
                eys_close: false,
                codeFlag: true,//是否重新获取验证码
                code: '', //验证码倒计时
                changeText: '获取验证码',
                timer1: null,
                isYzmFlag: false,//是否显示验证码
                isInputPwd: false, //是否显示短信验证码，和密码
                argeementFlag: false,//用户协议是否显示
                type: 1,//判断是否忘记注册验证码  1注册2忘记
            }
        },
        methods: {
            hrefArgeementPage () {
                this.argeementFlag = true;
            },
            fsl (e) { //input获取焦点
                e.target.focus()
            },
            getYzmVal () {//手机号输入事件
                let that = this;
                var patt = /^1[3456789]\d{9}$/;
                if(patt.test(this.form.user_mobile)){
                    this.jYZM();
                    that.isYzmFlag = true;
                } else {
                    $('.geetest_goto').each(function(){
                       $(this).remove()
                    });
                    that.isYzmFlag = false;
                    this.isInputPwd = false;
                }
            },
            eye_click: function () {
                this.eys_close = !this.eys_close
            },
            // sendQcode (e) {
            //     // console.log(md5('313131'));
            //     // let utoken = 'd36e379e-05d0-49c5-bc6a-406085c21c4b';
            //     // let token = md5(utoken);
            //     // this.form.token = token;
            //     // console.log(token);
            //     let that = this;
            //     var patt = /^1[3456789]\d{9}$/;
            //     // if (this.form.user_mobile) {
            //         // if(!patt.test(this.form.user_mobile)){
            //         //     layer.msg('请填写正确的手机号格式');
            //         //     return false;
            //         // }
            //         if (this.codeFlag) {

                        

            //             // this.$http.post(units.domin('Sms/forget'), units.params(this.form)).then(function (res) {
            //             //     if(!res.data.warning){
            //             //         if (res.data.code > 0) {
            //             //             layer.msg(res.data.info, 2, function () {
            //             //                 that.changetime();
            //             //             });
            //             //         } else {
            //             //             layer.msg(res.data.msg);
            //             //         }
            //             //     } else{
            //             //         layer.msg(res.data.warning)
            //             //     }
            //             // }, function () {//请求错误
            //             //     layer.open({
            //             //         content: '服务器响应错误'
            //             //         ,skin: 'msg'
            //             //         ,time: 1 //2秒后自动关闭
            //             //     });
            //             //     return;
            //             // });

            //         }
                    
            //     // } else {
            //     //     layer.msg('请检查手机号')
            //     // }
            // },
            changetime () {
                let that = this;
                const TIME_COUNT = 60;
                if (!this.timer1) {
                    this.changeNumber = TIME_COUNT;
                    this.codeFlag = false;
                    this.timer1 = setInterval(() => {
                        if (this.changeNumber > 1 && this.changeNumber <= TIME_COUNT) {
                            this.changeNumber--;
                        } else {
                            this.codeFlag = true;
                            this.changeText = '重新获取验证码';
                            clearInterval(this.timer1);
                            this.timer1 = null;
                        }
                    }, 1000)
                }
            },
            validate: function (fn) {
                let that = this;
                let tips = ['昵称', '手机号', '验证码', '密码'];
                let from = this.form;
                let num = -1;
                let next = false;
                $.each(from, function (k, value) {
                    num++;
                    if (!value && k != 'type') {
                        layer.msg('请检查' + tips[num]);
                        next = true;
                        return false;
                    }
                    if(k == 'user_mobile')
                    {
                        var patt = /^1[3456789]\d{9}$/;
                        if(!patt.test(value)){
                            layer.msg('请填写正确的'+tips[num]+'格式');
                            next = true;
                            return false;
                        }
                    }
                    if(k == 'user_password')
                    {
                        var patt = /^[0-9A-Za-z!-@#$%^&*￥.,?`~+=;}{)]{8,16}$/;
                        if(!patt.test(value)){
                            layer.msg('请填写正确的8-16位的'+tips[num]);
                            next = true;
                            return false;
                        }
                    }
                });
                fn && fn(next)
            },
            postData(){
                let that = this;
                this.validate(function (res) {
                    if (!res) {
                        if(!$("input[type='checkbox']").is(':checked')) {
                            layer.msg('请阅读用户注册协议');
                            return;
                        }
                        that.$http.post(units.host('Register'), units.params(that.form)).then(function (res) {
                            if (res.data.code > 0) {
                                cookie.set('user_id', res.data.msg.user_id);
                                cookie.set('user_nickname', res.data.msg.user_nickname);
                                cookie.set('user_token', res.data.msg.user_token)
                                //判断是否为大堂经理
                                if (res.body.msg.role == '1') {
                                    console.log('大堂经理', res)
                                    that.$store.state.isVIP = true
                                    localStorage.setItem("isVIP", true);
                                    
                                } else {    
                                    console.log('普通人')
                                    that.$store.state.isVIP = false
                                    localStorage.removeItem("isVIP")
                                }
                                layer.msg(res.data.info, 2, function () {
                                    // location.href = '#/metype'; //选择执行方还是委托方
                                    let nowTime = new Date()*1
                                    // let startTime = new Date(res.body.msg.sign_start_time).getTime()
                                    let endTime = new Date(res.body.msg.sign_end_time).getTime()
                                    if(nowTime < endTime && res.body.msg.sign_end_time) {
                                        cookie.set('sign_uesr', 2)//已签约
                                    } else {
                                        cookie.set('sign_uesr', 1)
                                    }
                                    location.href = '#/Authentication'; //身份验证
                                    
                                })
                            } else {
                                layer.msg(res.data.info + ',' + res.data.msg);
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
                })
            },
            forget: function () {
                let that = this;
                if(!that.form.user_mobile){
                    layer.msg('请检查手机号');
                    return false;
                }
                if(!that.form.qcode){
                    layer.msg('请检查验证码');
                    return false;
                }
                if(!that.form.user_password){
                    layer.msg('请检查密码');
                    return false;
                }
                that.$http.post(units.host('forget'), units.params(that.form)).then(function (res) {
                    if (res.data.code > 0) {
                        layer.msg(res.data.info, 2, function () {
                            location.href = '#/login';
                        })
                    } else {
                        // console.log(res.data);
                        layer.msg(res.data.info);
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
            next: function () {
                
                if (this.form.type == 1) {
                    this.forget();
                } else {
                    this.postData();
                }
            },
            jYZM () {  //极验显示
                var that = this; 
                var handlerEmbed = function (captchaObj) {
                    captchaObj.onSuccess(function () {
                        var result = captchaObj.getValidate();
                        // console.log(result)
                            $.ajax({//二次验证
                            // 获取id，challenge，success（是否启用failback）
                            url: "https://www.kkok.cn/index.php/api/sms/second_geetest", // 加随机数防止缓存
                            type: "POST",
                            dataType: "json",
                            data:{
                                geetest_challenge: result.geetest_challenge,
                                geetest_validate: result.geetest_validate,
                                geetest_seccode: result.geetest_seccode,
                                mobile: that.form.user_mobile,
                                type: that.type, //注册验证码
                                ///手机号码
                            },
                            success: function (data) {
                                console.log(data)
                            if(data.status ='success') {
                                layer.msg(data.info)
                                if(data.code > 0) {
                                    that.isInputPwd = true;
                                } else {
                                    that.isInputPwd = false;
                                }
                            }
                            if (data.status === 'fail') {
                                captchaObj.reset(); // 调用该接口进行重置
                            }
                                // 使用initGeetest接口
                                // 参数1：配置参数
                                // 参数2：回调，回调的第一个参数验证码对象，之后可以使用它做appendTo之类的事件
                            
                            }
                        });
                    })
                    // 将验证码加到id为captcha的元素里，同时会有三个input的值：geetest_challenge, geetest_validate, geetest_seccode
                    captchaObj.appendTo("#embed-captcha");
                    captchaObj.onReady(function () {
                        $("#wait")[0].className = "hide";
                    });
                    // 更多接口参考：http://www.geetest.com/install/sections/idx-client-sdk.html
                };
                $.ajax({
                    // 获取id，challenge，success（是否启用failback）
                    url: "https://www.kkok.cn/index.php/api/geetest/init_geetest?t=" + (new Date()).getTime(), // 加随机数防止缓存
                    type: "get",
                    dataType: "json",
                    success: function (data) {
                        console.log(data);
                        // 使用initGeetest接口
                        // 参数1：配置参数
                        // 参数2：回调，回调的第一个参数验证码对象，之后可以使用它做appendTo之类的事件
                        initGeetest({
                            gt: data.gt,
                            challenge: data.challenge,
                            new_captcha: data.new_captcha,
                            width: '8rem',
                            product: "embed", // 产品形式，包括：float，embed，popup。注意只对PC版验证码有效
                            offline: !data.success // 表示用户后台检测极验服务器是否宕机，一般不需要关注
                            // 更多配置参数请参见：http://www.geetest.com/install/sections/idx-client-sdk.html#config
                        }, handlerEmbed);
                    }
                });
            }
        },
        beforeRouteLeave (to, from, next) {
            // console.log(this.$refs.detailInfo)
            if( this.argeementFlag) {
                this.argeementFlag = false
                next(from.path)
                units.title.set('注册账号');
            } else {
                next()
            }
        },
        components: {UserAgreement},
        mounted(){   
            // console.log('mounted')
            
        },
        destroyed () {
            // console.log('destroyed')
        },
        deactivated () {
            // console.log('deactivated')
        },
        // activated () {

        //     this.$store.state.header.titleShow = true;
        //     this.form.type = this.$route.query.type;
            
        //     if(this.$route.query.isempty == '1'){
        //         // console.log(this.$route.query.isempty)
        //         this.form.qcode = '';
        //         this.form.user_password = '';
        //         this.form.user_mobile = '';
        //     }
        //     if (this.form.type) {
        //         units.title.set('忘记密码')
        //     } else {
        //         units.title.set('注册账号')
        //     }
        //     // console.log('activated');
        // },
        created: function () {
            // console.log('created');
            // console.log(gt)
            this.form.type = this.$route.query.type;
            if(this.$route.query.isempty == '1'){
                this.form.qcode = '';
                this.form.user_password = '';
                this.form.user_mobile = '';
            }
            if (this.form.type) {
                units.title.set('忘记密码')
                this.type = 2;
            } else {
                units.title.set('注册账号');
                this.type = 1;
            }
        }
    }
</script>
