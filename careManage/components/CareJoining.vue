<template>
<!-- 订单详情弹窗 -->
    <div class="go-care-box">
        <div class="go-care">
            <div class="go-care-dialog">
                <h6>车辆信息</h6>
                <div class="care-info-box">
                    <div class="care-car-brand">
                        <span class="title">车辆品牌：</span>
                        <span  class="content" v-if='false'>{{detailOrderData.card_brand?detailOrderData.card_brand.slice(0,10): '暂无'}}</span>
                        <span  class="content">{{detailOrderData.card_brand}}</span>
                    </div>
                    <div class="care-car-brand">
                        <span class="title">车辆号码：</span>
                        <span  class="content">{{detailOrderData.card_number?detailOrderData.card_number: '暂无'}}</span>
                    </div>
                    <div class="care-car-brand">
                        <span class="title">车辆颜色：</span>
                        <span  class="content">{{detailOrderData.card_color?detailOrderData.card_color: '暂无'}}</span>
                    </div>
                </div>
                <h6>看护人员填写</h6>
                <div class="care-info-box">
                    <div class="care-car-brand">
                        <span class="title">姓&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;名：</span>
                        <span  class="content">{{detailOrderData.nurse_name?detailOrderData.nurse_name: '暂无'}}</span>
                    </div>
                    <div class="care-car-brand" style="height:1.2rem;line-height:1.2rem;padding-top:0.2rem;vertical-align：middle;text-align: justify;
word-break: break-all;">
                        <span class="title">联系方式：</span>
                        <span  class="content" style="font-size: .53rem;">{{detailOrderData.nurse_phone?detailOrderData.nurse_phone: '暂无'}}</span>
                    </div>
                </div>
                <div class='btn' @click="closeCareDetalis"><button></button></div>
            </div>
        </div>   
    </div>
</template>

<script>
export default {
    props: ['detailOrderData'],
    methods: {
        closeCareDetalis () {
            this.$emit('cloCareDet')
        }
    },
}
</script>

<style lang='scss' scoped>
.go-care-box{
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, .5);
    z-index: 999;
    .close-x{
        position: absolute;
        bottom:-1.8rem;
        margin-left: 50%;
        transform: translateX(-50%);
    }
    .go-care{
        width: 8.5rem;
        position: absolute;
        top: 15%;
        background: #f0f4fa;
        margin-left: 50%;
        transform: translateX(-50%);
        border-radius: .08rem;
        .go-care-dialog{
            padding:0rem .6rem .8rem .6rem;
            h6{
                font-weight: bolder;
                padding: .4rem 0 .2rem 0;
            }
            .care-info-box{
                width: 100%;
                font-size: .5rem;
                background: #fff;
                border-radius: .08rem;
                padding-bottom:.3rem; 
                .care-car-brand{
                    padding: .3rem .3rem 0 .3rem;
                    display: flex;
                    .title{
                        color: #b4b4b4;
                        width: 2.5rem;
                    }
                    .content{
                        flex:1;
                        font-weight: 400;
                        color: #1f1f1f;
                    }
                }
            }
            .btn{
                margin-top : .6rem;
                width: 100%;
                height: 1.4rem;
                border-radius: .08rem;
                button{
                    width: 100%;
                    height: 100%;
                    outline: none;
                    border-radius: .08rem;
                    border: 0;
                    background: url('../../../assets/img/close-btn.png') center no-repeat;
                    background-size: 100%;
                }
            }
        }
    }
}
</style>
