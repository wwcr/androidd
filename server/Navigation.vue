<!--页面css样式-->
<style lang='scss'>
    .tion{
        padding: 0 .5rem;
        box-sizing: border-box;
        padding-top: $top +.5rem;
        .banner{
            width: 100%;
        }
        .banner img{
            width: 100%;
            height: 5.14rem;
            border-radius: .2rem;
        }
        .center{
            background: #fff;
            width: 100%;
            border-bottom-left-radius: .2rem;
            border-bottom-right-radius: .2rem;
            margin: 0 auto;
            padding: 0.3rem;
            -moz-box-shadow:4px 4px 12px 4px rgba(20%,20%,40%,0.2);
            -webkit-box-shadow:4px 4px 12px 4px rgba(20%,20%,40%,0.2);
            box-shadow:4px 4px 12px 4px rgba(20%,20%,40%,0.1);
            position: relative;
            top: -0rem;
            div{
                display: flex;
                font-size: .43rem;
                line-height: .7rem;
                margin-top: .19rem;
                .findCarOrder{
                    width: 3rem;
                }
                span{
                    flex:1;
                }
            }
        }
        .center p span{
            color: #1e1e1e;
        }
        .center p img{
            width: 0.5rem;
            vertical-align: middle;
            margin-top: -0.1rem;
            margin-right: 0.2rem;
        }
        .nav{
            text-align: center;
            margin-top: 2rem;
            .btn{
                display: flex;
                justify-content: space-between;
                button{
                    width: 4.1rem;
                    height: 1.4rem;
                    border-radius: .2rem;
                    color: #fff;
                    font-size: .55rem;
                    border:0;
                    outline: none;
                }
                .sure{
                    margin-left: .2rem;
                    background: #2c7dfe;
                }
                .cancle{
                    margin-right: .2rem;
                    background: #ff6e16;
                }
                
                .cancle-over{
                    background: #ccc;
                    color: #909090;
                }
            }
        }
        .nav img{
            width: 5.4rem;
        }
        .carsee-content{ //未付款前详情页
            display: flex;
            line-height: .5rem;
            padding: .5rem 0;
            background: #fff;
            .icon1{
                width: 2rem;
                height: .9rem;
                padding: 0 .2rem;
            }
            .icon2{
                // width: ;
                height: 1rem;
            }
            .text{
                font-size: .35rem;
                flex:1;
                b{
                    color: #ff9b0c;
                }

            }
        }
        .btn1{ //立即付款按钮
            width: 100%;
            height: 1.5rem;
            border-radius: .15rem;
            margin-top: 2rem;
            button{
                width: 100%;
                height: 100%;
                background: url('../../assets/img/btn-bg.png') center no-repeat;
                background-size: 100% 100%;
                outline: none;
                border:none;
                border-radius: .15rem;
                color: #fff;
                font-size: .5rem;
            }
        }
    }
    .swiper-pagination-bullet-active{ //轮播焦点
        width: .25rem;
        height: .25rem;
        display: inline-block;
        border-radius: 100%;
        background: #fff;
        position: static;
    }
    .gps-box-warn{
        color:#ff3535;
        font-size: .48rem;
        line-height: 1.1rem;
        background: #fff;
        font-weight: bolder;
    }
</style>
<!--导航前往-->
<template>
    <div class="tion">
        <div class="white">
            <div class="banner">
                <swiper v-if='cardata_IMG' :options="swiperOption" ref="mySwiperA">
                    <swiper-slide v-for="(x, ind) in banner_list1" :key='ind' >
                        <img style="height:5.65rem;" :src='host+x'>
                    </swiper-slide>
                    <div class="swiper-pagination"  slot="pagination"></div>
                    <!-- <div class="swiper-scrollbar"   slot="scrollbar"></div> -->
                </swiper>
                <swiper v-else :options="swiperOption" ref="mySwiperA">
                    <swiper-slide v-for="(x, ind) in banner_list" :key='ind' >
                        <img style="height:5.65rem;" :src='x'>
                    </swiper-slide>
                    <div class="swiper-pagination"  slot="pagination"></div>
                    <!-- <div class="swiper-scrollbar"   slot="scrollbar"></div> -->
                </swiper>
            </div>
            <div class="center clearfix" v-if='detailList.pay_status == 2'>
                <p class="gps-box-warn">请先下载“博云车联 V2”APP 登录后即使用</p>
                <div><p class="findCarOrder"><img src="../../assets/img/gps_admin.png">GPS账号：</p><span>{{detailList.cardata.car_gps?detailList.cardata.car_gps:'暂无GPS编号'}}</span></div>
                <div><p class="findCarOrder"><img src="../../assets/img/gps_pwd.png">GPS密码：</p><span>{{detailList.cardata.car_gpspassword?detailList.cardata.car_gpspassword:'暂无GPS密码'}}</span></div>
                <div><p class="findCarOrder"><img src="../../assets/img/img_34.png">拍照时间：</p><span>{{detailList.cardata.car_addtime?detailList.cardata.car_addtime:'暂无拍照时间'}}</span></div>
                <div><p class="findCarOrder"><img src="../../assets/img/img_33.png">发现位置：</p><span>{{detailList.cardata.car_location?detailList.cardata.car_location:'暂无显示位置'}}</span></div>
            </div>
            <div class="carsee-content" v-else>
                <img class="icon1" src="../../assets/img/icon5.png" alt="">
                <p class="text">本次服务需要交纳寻车服务费<b>{{price}}</b>元 才可查看车辆详情</p>
                <img class="icon2" src="../../assets/img/icon6.png" alt="">
            </div>
        </div>
        <div class="nav">
            <!-- <a class="mode" @click.stop="href('server/map')"><img src="../../assets/img/img_35.png"></a> -->
            <!-- <a class="mode" @click="selectmap()"><img src="../../assets/img/img_35.png"></a> -->
            <div class="btn" v-if='detailList.pay_status == 2'><!--  是否支付寻车费用 -->
                <button class="cancle" v-if='detailList.isNurse =="true"' @click='platformCare()'>平台看护</button><!--  是否过了24小时 -->
                <button class="cancle-over" v-else >平台看护</button><!--  是否过了24小时 -->
                <button class="sure" @click='selectmap'>导航前往</button>
            </div>
            <div class="btn1" v-else @click="payment()"><button>立即付款</button></div>
        </div>
    </div>
</template>
<script>
    import units from '../../tools/units';
    import cookie from '../../tools/cookie';
    import headers from '../template/header.vue';
    export default {
        name: 'index',
        data () {
            return {
                serverType: 1,
                list: [],
                articlePage: 1,
                articleLimit: 12,
                moreThat: true,
                host: units.getHost(),
                current: [true, false, false],
                currentNum: 1,
                sid: '',
                search: false,
                status: 1,
                searchKeyword: '',
                show: true,
                count: '',
                timer: null,
                car_addtime:'',
                car_location:'',
                long:'',
                lat:'',//纬度
                pic:'',
                price: '3800',
                cardata_IMG:'',//寻车图片拍摄
                sniff: {},//判断设备
                detailList: {},//详情数据
                banner_list: [require('../../assets/img/banner1.png'), require('../../assets/img/banner2.png')],//本地图片轮播
                banner_list1: [], //线上图片数据
                swiperOption: {
                    // autoplay: 5000,
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
            }
        },
        components: {
            headers
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
                    that.list = res.info.data;
                    that.moreThat = false;
                })
            }
        },
        methods: {
            platformCare () { //平台看护
                console.log(this.detailList)
                location.href = '#/server/platformCare?data='+JSON.stringify(this.detailList);
            },
            payment () {//寻车付款
                let find_id = this.$route.query.find_id;
                let id = this.$route.query.id;
                // if(cookie.get('sign_uesr') == 2) { //签约用户==》以后实现
                //     location.href= '#/find/paysuccess';
                // } else {  
                //     this.href('pay?type=2&order='+this.detailList.card_order+'&id='+id+'&find_id='+find_id)
                // }
                this.href('pay?type=2&order='+this.detailList.card_order+'&id='+id+'&find_id='+find_id)
            },
            getCarInfo () { //获取车辆详情
                let find_id = this.$route.query.find_id;
                let id = this.$route.query.id;
                this.$http.post(units.host('get_finded_pic', 'Api'), units.paramsno({
                    find_id,
                    id
                })).then(function (res) {
                    this.detailList = res.body;
                    this.cardata_IMG = res.body.cardata;
                    // console.log(cardata)
                    if(res.body.cardata.car_img) {  
                        this.banner_list1 = JSON.parse(res.body.cardata.car_img);
                    }
                    // this.long = res.body.gpsdata[0];
                    // this.lat = res.body.gpsdata[1];
                    this.long = res.body.longitude;
                    this.lat = res.body.latitude;
                    this.car_addtime = res.body.car_addtime;
                    this.car_location = res.body.car_location;
                }, function () {//请求错误
                    layer.open({
                        content: '服务器响应错误'
                        ,skin: 'msg'
                        ,time: 1 //2秒后自动关闭
                    });
                    return;
                });
            },
            gotorun:function (x) {
                location.href = '#/server/details?cid='+x.find_id;
            },
            selectmap () {//导航前往
                let that = this;
                
                layer.tips(["百度地图","高德地图"],'',function (e) {
             	    console.log(e);
                    if(e == '百度地图'){
                         var loadDateTime = new Date();//获取当前时间
                         window.setTimeout(function() {  
                            var timeOutDateTime = new Date(); //获取定时器执行时的时间
                            if (timeOutDateTime - loadDateTime < 5000) {  //定时器  时间太久就不跳转了
                            if(that.sniff.android) {  //判断设备
                                layer.msg('请安装'+e);
                                return;
                            } else if(that.sniff.ios){  //跳到app store进行下载
                                window.location = "itms-apps://itunes.apple.com/cn/app/id452186370?ls=1&mt=8";//ios下载地址  
                            }
                            } else {  
                                window.close();  
                            }  
                         },1000); //设置1S看看 原理 如果安装应用了跳转了就不会执行定时器 时间久不跳转就执行定时器
                        if(that.sniff.android) {  //判断设备
                            //  window.location = "bdapp://map/geocoder?address="+that.car_location+"&src=webapp.geo.yourCompanyName.yourAppName";
                            window.location = "bdapp://map/geocoder?src=openApiDemo&address="+that.car_location;
                             
                        } else if(that.sniff.ios){  
                           window.location.href = "baidumap://map/geocoder?address="+that.car_location+"&src=webapp.geo.yourCompanyName.yourAppName";
                        }
                        
                    }else{
                        var loadDateTime = new Date();//获取当前时间
                         window.setTimeout(function() {  
                            var timeOutDateTime = new Date(); //获取定时器执行时的时间
                            if (timeOutDateTime - loadDateTime < 5000) {  //定时器  时间太久就不跳转了
                                if(that.sniff.android) {  //判断设备
                                    layer.msg('请安装'+e);
                                    return;
                                } else if(that.sniff.ios){  //跳到app store进行下载
                                    window.location = "itms-apps://itunes.apple.com/cn/app/id461703208?mt=8";//ios下载地址  
                                }
                                
                            } else {  
                                window.close();  
                            }  
                        },1000); 
                        if(that.sniff.android) {  //判断设备
                        // console.log("androidamap://navi?sourceApplication=appname&poiname=fangheng&lat="+that.lat+"&lon="+that.long+"&dev=1&style=2")
                            window.location = "androidamap://navi?sourceApplication=appname&poiname=fangheng&lat="+that.lat+"&lon="+that.long+"&dev=1&style=2";
                        } else if(that.sniff.ios){  //跳到app store进行下载
                            window.location.href = "iosamap://navi?sourceApplication=appname&poiname=fangheng&lat="+that.lat+"&lon="+that.long+"&dev=1&style=2";
                        }
                   
                    }
                });
            },
            priceShow () {
                this.$http.post(units.host('get_sale', 'api'), units.paramsno({
                    type: 1,//1==》寻车定位 2==》看护
                })).then( function (res) {
                    this.price = res.body.info[0].current_money;
                })
            }
        },
        mounted(){
            // let id = this.$route.query.id; //之前的代码
            // this.$http.post(units.host('get_finded_pic','api'), {
            //         id: id//穿车牌
            //     }).then(function (res) {
            //         this.car_addtime = res.body.car_addtime;
            //         this.car_location = res.body.car_location;
            //         this.pic = units.getHost() + res.body.car_photo;
                    
            //     });
           
        },
        created () {
            units.title.set('车辆详情');
            this.$store.state.header.left = function () {
                location.href = '#/server/content?cur=3';
            };
            this.sniff =require('@/tools/sniff');
            this.getCarInfo();
        }
}
</script>
