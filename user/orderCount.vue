<!--订单统计-->
<template>
    <div class="find">
        <div class="connection-box">
            <div class="shot-number-box">
                 <div class="sum-box">
                    <p class="sum-title">订单完成总额度</p>
                    <p class="price"><b>{{orderMoney.total_money}}</b><small>元</small></p>
                </div>
                <div class="shot-number">
                    <span class="shot-single">
                        <span class="shot-title">回收中订单数</span>
                        <b>{{orderMoney.order_num_status1}}</b>
                    </span>
                    <span class="shot-single">
                        <span class="shot-title">交接中订单数</span>
                        <b>{{orderMoney.order_num_status2}}</b>
                    </span>
                    <span class="shot-single">
                        <span class="shot-title">已完成订单数</span>
                        <b>{{orderMoney.order_num_status4}}</b>
                    </span>
                </div>
            </div>
        </div>
    </div>
</template>
<script type="text/javascript">
    import Vue from 'vue';
    import units from '../../tools/units'
    import cookie from '@/tools/cookie';
    export default {
        name: 'index',
        data () {
            return {
                flag:true,
                current:1,
                orderMoney: {} //订单总额
            }
        },
        methods:{
            getOrderMoneyData(){
                this.$http.post(units.host('statisticsOrderByUser'), {
                    user_id: cookie.get('user_id'),
                    role: cookie.get('role'),
                    order_by: this.order_by 
                }).then(function (res) {
                    // console.log(res)
                    this.orderMoney = res.body.info
                });
            },
        },
        created: function () {
            this.getOrderMoneyData()
            units.title.set('订单统计');
            this.$store.state.header.left = function () {
                location.href = '#/user/index';
            };
        }
    }
</script>

<!--页面css样式-->
<style scoped lang='scss'>
    .header {
        /*margin-top: 0.3rem;*/
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
    .header > p {
        text-align: center;
        font-size: 0.44rem;
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
        color: #fff;
        margin-left: 1rem;
        margin-right: 1rem;
        height: 1.25rem;
    }

    .header > p a {
        color: #fff;
        padding: 0.1rem 0.5rem;
        border-radius: 0.5rem;
        margin-left: 0.6rem;
        margin-right: 0.6rem;
    }

    .header > p a.currer {
        color: #fff;
        padding: 0.1rem 0.5rem;
        background: #5395fd;
        border-radius: 0.5rem;
        margin-left: 0.6rem;
        margin-right: 0.6rem;
    }
    .connection-box{
        padding-top:1.25rem; 
        padding:1.25rem .4rem 0 .4rem;
        font-size: .5rem;
        background: #f0f4fa;
        .shot-number-box{
            margin-top: .6rem;
            background: #fff;
            padding:0 .4rem; 
            border-radius: .2rem;
            .sum-box{
                text-align: center;
                height: 3rem;
                .sum-title{
                   padding-top: .7rem;
                   font-size: .4rem;
                   font-weight: bold;
                }
                .price{
                    color:#2c7dfe;
                    margin-top:.2rem; 
                     b{
                        font-size: .75rem;
                        margin-right: .2rem;
                    }
                }
            }
            h5{
                font-size: .52rem;
                line-height: 1.5rem;
            }
            .shot-number{
                border-top: .01rem solid #eee;
                display: flex;
                justify-content: space-between;
                .shot-single{
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    flex-direction: column;
                    .shot-title{
                        font-size: .35rem;
                        padding-top:.35rem; 
                    }
                    b{
                        color:#2c7dfe;
                        line-height: 1.2rem;
                    }
                }
                
            }
        }
        .shot-number-box-only{
            padding-bottom: 1rem;
        }
    }
</style>