<template>
    <div class="carsee-box">
        <div class="carsee-al-ccontent">
            <div class="carsee-ccontent-bg">
                <div class="banner-box">
                    <swiper v-if='banner_list1' :options="swiperOption" ref="mySwiperA">
                        <swiper-slide v-for="(x, ind) in banner_list1" :key='ind' >
                            <img style="height:5.65rem;" :src='host+x.banner'>
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
                <div class="carsee-content">
                    <img class="icon1" src="../../assets/img/icon5.png" alt="">
                    <p class="text">本次服务需要交纳寻车服务费<b>2800</b>元 才可查看车辆详情</p>
                    <img class="icon2" src="../../assets/img/icon6.png" alt="">
                </div>
            </div>
            <div class="btn"><button>立即付款</button></div>
        </div>
    </div>
</template>

<script>
import units from '@/tools/units';
import { swiper, swiperSlide } from 'vue-awesome-swiper'
export default {    
    data () {
        return {
            detailList: {},//详情数据
            banner_list: [require('../../assets/img/banner.png'), require('../../assets/img/banner.png'), require('../../assets/img/banner.png')],//本地图片轮播
            banner_list1: [], //线上
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
    methods: {
        getCarInfo () {
            let find_id = this.$route.query.find_id,
                id = this.$route.query.id;
            this.$http.post(units.host('get_finded_pic', 'Api'), units.params({
                find_id,
                id
            })).then(function (res) {
                this.detailList = res.body;
                this.banner_list1 = res.body.cardata.car_img;
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
    created () {
        units.title.set('车辆详情');
        this.$store.state.header.left = function () {
                location.href = '#/server/content?cur=2';
            };
        this.getCarInfo();
    }
}
</script>

<style lang='scss'>
    .swiper-pagination-bullet-active{
        width: .25rem;
        height: .25rem;
        display: inline-block;
        border-radius: 100%;
        background: #fff;
        position: static;
    }
    .carsee-box{
        width:100%;
        padding-top:$top; 
        .carsee-al-ccontent{
            padding: .4rem;
            box-sizing: border-box;
            .carsee-ccontent-bg{  
                background: #fff;
                .banner-box{
                    width:100%;
                    // height: 5rem;
                    border-radius: .15rem;
                    img{
                        width:100%;
                        height: 100%; 
                        border-radius: .15rem;
                    }
                }
                .carsee-content{
                    display: flex;
                    line-height: .5rem;
                    padding: .5rem 0;
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
            }
            .btn{
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
    }
</style>
