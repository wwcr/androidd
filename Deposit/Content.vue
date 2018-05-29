
<template>
    <!--委托寻车押金页面-->
    <div class="deposit-content-box paddingTop">
        <div class="deposit-content">
            <p>
                (1)押金说明：寻车服务押金为使用无维易寻寻车服务保证金，押金额为{{price}}元。如果您不同意支付该押金，则不能使用该项功能。  
            </p>
            <p>
                (2)支付方式：目前缴纳押金方式为微信支付。  
            </p>
            <p>
                (3)使用权利：使用寻车服务需按规定支付该押金后方可使用该功能。  
            </p>
            <p>
                (4)押金用途：押金主要在用户发布委托寻车需求后，无维易寻为您寻找到该车辆后用户未进行支付寻车费用，系统将在24小时后将押金作为寻车费用进行支付。  
            </p>
            <p>
                (5)补充押金：如用户押金已被作为寻车费支付，用户如继续使用寻车业务，需支付规定金额的押金，支付押金后寻车功能可继续使用
            </p>
        </div>
        <div class="deposit-warn">
            <p class="warn"><img src="../../assets/img/deposit-warn.png">退款提示</p>
            <p class="info">如需退押金请联系客服客服电话：{{$store.state.phone}}</p>
        </div>
    </div>
</template>

<script>
    import units from '@/tools/units'
    export default {
        name: 'deposit',
        data () {
            return {
                price: 3500
            }
        },
        created (){
            units.title.set('押金协议');
            this.price = this.$route.query.price;
        },
    }
    
</script>

<!--页面css样式-->
<style scoped lang='scss'>  
    @import url("../../assets/style/paddingTop.css");
    
    .deposit-content-box{
        background: #fff;
        font-size: .5rem;
        .deposit-content{
            box-sizing: border-box;
            padding:.8rem .6rem ;
            padding-bottom: 4.2rem; 
            p{
                font-weight: bold;
                padding-bottom:1rem;
                line-height: .7rem; 
                &:last-child{
                    padding: 0;
                }
            }
        }
        .deposit-warn{
            background: #ebebeb;
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            font-size: .45rem;
            padding:.3rem .6rem  .5rem;
            box-sizing: border-box;
            .warn{
                font-weight: 800;
                font-size: .55rem;
                img{
                    width: .85rem;
                    height: auto;
                    margin-right:.3rem; 
                    position: relative;
                    top: -.09rem;
                }
            }
            .info{
                font-size: .4rem;
                margin-top: .2rem;
            }
        }
    }
</style>