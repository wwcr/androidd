<template>
    <div class="platform-care">
        <div class="care-content-box">
            <div class="care-ul" v-if='careData.find_id'>
                 <div class="care-li">
                    <div class="care-title">车辆品牌：</div>
                    <div class="care-content">{{careData.card_brand? careData.card_brand:'暂无'}}</div>
                </div>
                <div class="care-li">
                    <div class="care-title">车辆号码：</div>
                    <div class="care-content">{{careData.card_number? careData.card_number:'暂无'}}</div>
                </div>
                <div class="care-li">
                    <div class="care-title">车辆颜色：</div>
                    <div class="care-content">{{careData.card_color? careData.card_color:'暂无'}}</div>
                </div>
            </div>
            <p class="explain">说明:本次看护车辆为24小时，请及时联系看护人员办理交接手续</p>
            <div class="care-btn" @click="careFn()"><button></button></div>
        </div>
    </div>
</template>

<script>
import units from '@/tools/units'
import cookie from '@/tools/cookie'
export default {
    name: 'PlatformCare',
    data () {
        return {
            careData: {}
        }
    },
    methods: {
        careFn () {
            // if(cookie.get('sign_uesr') == 2) { //签约用户---以后
            //     location.href= '#/carnurse/success';
            // } else {  
            //     location.href = '#/server/pay?id='+this.careData.find_id+'&order='+this.careData.card_order;
            // }
            location.href = '#/server/pay?id='+this.careData.find_id+'&order='+this.careData.card_order;
            
        }
    },
    mounted(){
            // let order = this.$route.query.order;
            let find_id = this.$route.query.id;
            let that = this;
            console.log(navigator.userAgent)
            if(this.careData.find_id) {
                // var set_id = setInterval(function(){
                //     that.$http.post(units.domin('Nurse/paystatus'), {
                //         find_id,
                //         switch: 'nurse'
                //     }).then(function (res) {
                //         if(res.body.code == 2){
                //             clearInterval(set_id);
                //             location.href= '#/server/cansuccess';
                //             return false;
                //         }//该订单已支付
                //     });
                // },1000);//  
            }         
    },
    created () {
        units.title.set('看护管理');
        this.careData = JSON.parse(this.$route.query.data);
        console.log(this.careData)
        this.$store.state.header.left = function () {
            location.href = '#/server/content?cur=2';
        };
    }
}
</script>

<style lang='scss' scoped>
.platform-care{
    padding-top: $top;
    font-size: .5rem;
    .care-content-box{
        background: #f0f4fa;
        padding: .4rem;
        .care-ul{
            background: #fff;
            padding-bottom:.45rem;
            .care-li{
                display: flex;
                padding-top:.45rem;
                .care-title{
                    width: 3rem;
                    color: #787878;
                    padding-left:.45rem; 
                }
                .care-content{
                    color: #1e1e1e;
                    flex:1;
                }
            }
        }
        .explain{
            color: #ff3535;
            margin-top: .4rem;
            font-size: .4rem;
            line-height: .6rem;
        }
    }
    .care-btn{
        margin-top: .8rem;
        border-radius: .25rem;
        width: 100%;
        height: 1.2rem;
        button{
            border-radius: .25rem;
            width: 100%;
            height: 100%;
            border:0;
            outline: none;
            background: url(../../../assets/img/care-btn.png) center no-repeat;
            background-size: 100% 100%;
        }
    }
}
</style>
