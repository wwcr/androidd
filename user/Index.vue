
<!--个人中心-->
<template>
    <div class="personal">
        <div class="per_top">
            <span class="setting" @click="href('user/setting')">设置</span>
            <img src="../../assets/img/img_37.jpg">
            <div class="header-bg" v-if="info.user_header">
                <img style="border-radius:50%" :src="host+info.user_header">
            </div>
            <div class="header-bg" v-else>
              <img src="../../assets/img/img_38.png">
            </div>
            <p @click="outUser">{{info.user_mobile}}</p>
        </div>
        <div class="in_list">
            <ul>
                <li>
                    <a>
                        <img src="../../../src/assets/img/group_icon.png">
                        <label>资料认证</label>
                        <!-- 个人已认证,需要升级企业认证 -->
                        <span v-if ="info.user_anthen == 1" @click="companyAuthentication('Authentication_detail')">
                            <span class="arrow_right"></span>
                            <span class="message">
                                <p>{{info.auth.showButtonCenter}}</p>
                            </span>
                        </span>
                        <!-- 个人认证审核中， 企业认证审核中  企业已认证-->
                        <span v-if='info.user_anthen == 3 || info.user_anthen == 4 || info.user_anthen == 2'  @click="companyAuthentication('Authentication_detail')">
                            <span class="arrow_right"></span>
                            <span class="message">
                                <p>{{info.auth.showButtonCenter?info.auth.showButtonCenter:'企业已认证'}}</p>
                            </span>
                        </span>
                        <!-- 个人、企业认证失败 -->
                        <span v-if='info.user_anthen == -1 || info.user_anthen == -2'  @click="companyAuthentication('Authentication_detail?iswrite=1')">
                            <span class="arrow_right"></span>
                            <span class="message">
                                <p>{{info.auth.showButtonCenter}}</p>
                            </span>
                        </span>
                        <!-- 未认证 -->
                        <span v-if ="info.user_anthen == 0" @click="companyAuthentication('Authentication')">
                            <span class="arrow_right"></span>
                            <span class="message">
                                <p>{{info.auth.showButtonCenter?info.auth.showButtonCenter: '未认证'}}</p>
                            </span>
                        </span>
                    </a>
                </li>
                <!-- <li>
                    <a @click="href('user/firmname?t='+info.auth.per_workunit)">
                        <img src="../../../src/assets/img/group_icon2.png">
                        <label>企业名称</label>
                        <span class="arrow_right"></span>
                        <span class="message" v-if="info.auth != null || info.auth != undefined">
                            <p v-if="info.auth.per_workunit">{{info.auth.per_workunit}}</p>
                            <p v-else>{{info.auth.en_name}}</p>
                        </span>
                    </a>
                </li> -->
                <!-- <li v-if="isVIP"> -->
                <li v-if="false">
                    <a @click="href('user/myteam')">
                        <img src="../../../src/assets/img/group_icon8.png">
                        <label>员工管理</label>
                        <span class="arrow_right"></span>
                        <!-- <span class="message" v-if="info.auth != null">
                            <p v-if="info.auth.per_workunit">{{info.auth.per_workunit}}</p>
                            <p v-else>{{info.auth.en_name}}</p>
                        </span> -->
                    </a>
                </li>
                <!-- <li v-if="isVIP">
                    <a @click="href('user/datacollection')">
                        <img src="../../../src/assets/img/group_icon7.png">
                        <label>数据总览</label>
                        <span class="arrow_right"></span>
                         <span class="message" v-if="info.auth != null">
                            <p v-if="info.auth.per_workunit">{{info.auth.per_workunit}}</p>
                            <p v-else>{{info.auth.en_name}}</p>
                        </span>
                    </a>
                </li> -->
                <li v-if="isVIP">
                    <a @click="vipFn('caremanage?type=1')">
                        <img src="../../../src/assets/img/group_care.png">
                        <label>看护订单</label>
                        <span class="arrow_right"></span>
                        <!-- <span class="message" v-if="info.auth != null">
                            <p v-if="info.auth.per_workunit">{{info.auth.per_workunit}}</p>
                            <p v-else>{{info.auth.en_name}}</p>
                        </span> -->
                    </a>
                </li>
                <li v-if="isVIP">
                    <a @click="vipFn('user/devicemanagement')">
                        <img src="../../../src/assets/img/group_sb.png">
                        <label>设备管理</label>
                        <span class="arrow_right"></span>
                        <!-- <span class="message" v-if="info.auth != null">
                            <p v-if="info.auth.per_workunit">{{info.auth.per_workunit}}</p>
                            <p v-else>{{info.auth.en_name}}</p>
                        </span> -->
                    </a>
                </li>
                <!-- 订单总值 -->
                <!-- <li>
                    <a @click="href('user/ordercount')">
                        <img src="../../../src/assets/img/group_icon7.png">
                        <label>订单总值</label>
                        <span class="arrow_right"></span>
                    </a>
                </li> -->
                <li v-if="false">
                    <a>
                        <img src="../../../src/assets/img/group_icon3.png">
                        <label>员工职位</label>
                        <span class="arrow_right_2"></span>
                        <span class="message" v-if="info.auth">
                            <p>{{info.auth.per_worker||'暂无'}}</p>
                        </span>
                        <span v-else>
                            <a @click="href('authentication')">未认证</a>
                        </span>
                    </a>
                </li>
                <li v-if="false">
                    <a>
                        <img src="../../../src/assets/img/group_icon4.png">
                        <label>设置捆绑</label>
                        <span class="arrow_right"></span>
                        <span class="message">
                            <p class="p_p1" onclick="layer.msg('正在进行中,请稍等...')">开始捆绑</p>
                        </span>
                    </a>
                </li>
                <li v-if="false">
                    <a>
                        <img src="../../../src/assets/img/group_icon5.png">
                        <label>设备状态</label>
                        <span class="arrow_right"></span>
                        <span class="message">
                           <p class="p_p1" onclick="layer.msg('正在准备中,请稍等...')">查看</p>
                        </span>
                    </a>
                </li>
            </ul>
        </div>
        <div class="in_list" style="margin-bottom: 4rem;">
            <ul>
                <li>
                    <a>
                        <img src="../../../src/assets/img/group_icon6.png">
                        <label>客服电话</label>
                        <span>
                            <span class="arrow_right_2"></span>
                            <span class="message">
                                <p @click="tel()">{{$store.state.phone}}</p>
                            </span>
                        </span>
                        <!-- <span v-else>
                            <span class="message">
                                <a ><p style="color:#b4b4b4">{{$store.state.phone}}</p></a>
                            </span>
                        </span> -->
                    </a>
                </li>
            </ul>
        </div>
        <navcate></navcate>
        <messagesBox 
            v-if='telFlag'
            @cancelTel = 'cancelTel'
        />
    </div>
</template>
<script>
    import units from '../../tools/units'
    import cookie from '../../tools/cookie'
    import navcate from '../template/navcate.vue'
    import messagesBox from '@/components/frame/messagesBox'
    export default {
        name: 'index',
        data () {
            return {
                telFlag: false,
                sniff: {}, //判断设备
                warning:'233',//是否给予警告信息
                info: {
                    auth: {}
                },
                isVIP: false  //是否大堂经理
            }
        },
        components: {
            navcate,
            messagesBox
        },
        methods: {
            companyAuthentication (url) { //店家资料认证
                let that = this;
                if(!that.warning) {
                    location.href = '#/' + url
                } else {
                    layer.msg(that.warning);
                    return;
                }
            },
            vipFn (url) {//是否是大区经理的导航
                if( !this.info.enterAuth ) {
                    layer.msg('请先进行资料认证')
                    return false;
                }
                location.href = '#/' + url;
            },
            tel () { //电话弹窗是否出现
                this.telFlag = true  
            },
            cancelTel (val) { //是否确认拨打电话
                if (val) { //拨打电话
                    // if(this.sniff.android) {  //判断设备
                        // window.android.callAndroid ($store.state.phone);
                    // } else if(this.sniff.ios){
                        window.location.href = 'tel:'+this.$store.state.phone;
                    // }
                        
                }
                this.telFlag = false  
            },
            outUser: function () {
                let that = this;
                layer.open({
                    content: '退出当前账号',
                    btn: ['退出账号', '切换账号'],
                    yes: function () {
                        that.delCook(function () {
                            location.href = '/login';
                        });
                    },
                    no: function () {
                        that.delCook(function () {
                            location.href = '/';
                        });
                    }
                });
            },
            delCook: function (fn) {
                cookie.del('user_id');
                cookie.del('user_nickname');
                cookie.del('user_token');
                fn & fn();
            },
            len: function (str) {
                return str.substring(0, 10);
            },
            getdata: function () {
                this.$http.post(units.host('user_new'), units.params({
                    sw: 'info'
                })).then(function (res) {
                    // console.log(res.data.info.user_anthen)
                    this.info = res.data.info;
                    this.warning = res.data.warning;//是否给予警告信息
                    cookie.set('user_auth', res.data.info.user_anthen)
                    localStorage.setItem("infoData",JSON.stringify(this.info));
                });
            },
            startScroll () {
                document.getElementsByTagName("html")[0].style.overflow="visible";
                // document.getElementsByTagName("html")[0].style.height="auto";
                document.getElementsByTagName("body")[0].style.overflow="visible";
                // document.getElementsByTagName("body")[0].style.height="auto";
                // $('html').scrollTop(this.scrollTop);
                
            },
        },
        created: function () {
            units.title.set('个人中心');
            this.startScroll();
            this.sniff =require('@/tools/sniff');
            if(window.navigator.onLine==true){  //未联网状态跳转错误页
                this.getdata();
            } else {
                this.info = JSON.parse(localStorage.getItem("infoData"))
            }
            units.isLogin(true);
            cookie.set('curr',3);
            if(localStorage.getItem("isVIP")){
                this.isVIP = localStorage.getItem("isVIP")
                // console.log(this.isVIP)
            } else {
                this.isVIP = this.$store.state.isVIP
            }
        },
        beforeCreate: function () {
        },
    }
</script>
<!--页面css样式-->
<style scoped lang='scss'>
    .per_top {
        width: 100%;
        position: relative;
    }

    .per_top div.header-bg {
        /*background: url("../../assets/img/img_38.png") no-repeat;*/
        background-size: auto 100%;
        background-origin: border-box;
        background-position: center center;
        height: 2.8rem;
    }

    .per_top img {
        width: 100%;
        height: 6.63rem;
    }

    .per_top p {
        position: absolute;
        color: #fff;
        bottom: 1.3rem;
        left: 31%;
        font-size: 0.4rem;
        width: 37%;
        text-align: center;
    }

    .per_top div {
        width: 50%;
        margin: 0 auto;
        position: absolute;
        top: 25%;
        left: 25%;
        text-align: center;
    }

    .per_top div img {
        width: 2.2rem;
        height: 2.2rem;
        line-height: 2.8rem;
        border-radius: 50%;
        display: block;
        margin: 0 auto;
        margin-top: 0.3rem;
    }

    .in_list {
        background: #fff;
        border-top: 1px solid #f1f1f1;
        border-bottom: 1px solid #f1f1f1;
        margin-top: 0.3rem;
    }

    .in_list:last-child {
        border-bottom: none;
    }

    .in_list li {
        height: 1.49rem;
        border-bottom: 1px solid #f1f1f1;
        overflow: hidden;
        margin-left: 0.4rem;
        &:last-child{
            border:none;
        }
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
        font-size: 0.4rem;
        color: #1e1e1e;
    }

    .in_list .message {
        position: relative;
        float: right;
        margin: 0;
        height: auto;
        width: 50%;
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
        color: #d3d5dc;
        font-size: 0.48rem;
        line-height: 1.48rem;
        display: inline-block;

    }

    .in_list li a .arrow_right {
        position: relative;
        display: block;
        width: 0.7rem;
        height: 1.48rem;
        background: url(../../assets/img/img_14.png) no-repeat;
        background-position: right center;
        background-size: auto 30%;
        float: right;
    }

    .in_list li a .arrow_right_2 {
        position: relative;
        display: block;
        width: 0.7rem;
        height: 1.48rem;
        background-position: right center;
        background-size: auto 30%;
        float: right;
    }

    .in_list li a img {
        width: 0.5rem;
        vertical-align: middle;
        margin-top: 0.1rem;
    }

    .message p {
        font-size: 0.4rem;
        color: #1e1e1e;
        width: 40%;
    }

    .message p.p_p1 {
        color: #e24a4a;
    }

    .message p {
        text-align: right;
        float: right;
        width: 100%;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
    }
    .setting{
        position: absolute;
        right: 0.6rem;
        top: 0.4rem;
        color: #ffffff;
        font-size: 0.4rem;
    }

</style>