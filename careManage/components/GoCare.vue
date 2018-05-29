
<template>
<!-- 去看护弹窗 -->
    <div class="go-care-box">
        <div class="go-care">
            <div class="go-care-dialog">
                <h6>车辆信息</h6>
                <div class="care-info-box" v-if='careData.brand'>
                    <div class="care-car-brand">
                        <span class="title">车辆品牌：</span>
                        <span  class="content">{{careData.brand?careData.brand: '暂无'}}</span>
                    </div>
                    <div class="care-car-brand">
                        <span class="title">车辆号码：</span>
                        <span  class="content">{{careData.card?careData.card: '暂无'}}</span>
                    </div>
                    <div class="care-car-brand">
                        <span class="title">车辆颜色：</span>
                        <span  class="content">{{careData.card_color?careData.card_color:'暂无'}}</span>
                    </div>
                </div>
                <h6>看护人员填写</h6>
                <div class="input-care-name">
                    <input type="text" placeholder="请输入看护人员姓名" v-model ='info.name'>
                </div>
                <div class="input-care-name">
                    <input type="tel" placeholder="请输入看护人员联系方式"  v-model ='info.tel'>
                </div>
                <div class='btn' @click="goCare (1)"><button></button></div>
            </div> 
            <div class="close-x" @click="careClose(0)">
                <img src="../../../assets/img/xxxx.png" alt="">
            </div>
        </div>   
    </div>
</template>

<script>
export default {
    name: 'Gocare',
    props: ['careData'],
    data () {
        return {
            info: {
                name: '',
                tel: '',
                find_id: ''
            }
        }
    },
    methods: {
        goCare (val) { //点击看护
            let that = this;
            this.validate(function (ress) {
                if (ress) {
                    var patt = /^1[3456789]\d{9}$/;
                    if(!patt.test(that.info.tel)){
                        layer.msg('请填写正确的手机号');
                        return false;
                    }
                    that.$emit('goCareFn', {info: that.info, val: val})
                }
            }, $('input'))
        },
        careClose (val) {
            this.$emit('goCareFn', val)
        },
        validate: function (fn, midia) {
            let flag = true;
            let len = midia.length;
            for (var i = 0; i < len; i++) {
                if (!midia.eq(i).val()) {
                    let tips = midia.eq(i).attr('placeholder');
                    layer.msg(tips);
                    flag = false;
                    break;
                }
            }
            fn && fn(flag);
        },
    },
    created () {
        this.info.find_id = this.careData.find_id;
    }
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
        top: 12%;
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
            .input-care-name{
                width: 100%;
                height: 1.3rem;
                border-radius: .08rem;
                border: .01rem solid #cbd4e1;
                margin-bottom: .5rem; 
                input{
                    font-size: .5rem;
                    padding: .33rem .5rem;
                    border-radius: .08rem;
                    width: 100%;
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
                    background: url('../../../assets/img/wait-care-btn.png') center no-repeat;
                    background-size: 100%;
                }
            }
        }
    }
}
</style>
