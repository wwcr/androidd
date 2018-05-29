<template>
    <div class="warn-mark">
        <div class="warn-box">
            <h5>提示</h5>
            <p>是/否要取消订单</p>
            <div class="btn">
                <button class="cancle" @click=close(0)>取消</button>
                <button class="sure" @click=close(1)>确定</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'warnAlert',
    methods: {
        close (id) {//是否关闭
            this.$emit('close', id)
        }
    }
}
</script>

<style scoped lang='scss'>
    .warn-mark{
        position: fixed;
        top: 0;
        right: 0;
        left: 0;
        bottom: 0;
        background: rgba(0,0,0,.5);
        z-index: 999;
        .warn-box{
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%,-50%);
            width: 8.5rem;
            height: 7rem;
            border-radius: .18rem;
            background: #fff;
            font-size: .6rem;
            text-align: center;
            h5{
                color: #ff3520;
                font-weight: bolder;
                line-height: 2.5rem;
                font-size: .8rem;
            }
            p{
                color: #5a5a5a;
            }
            .btn{
                padding: 1.5rem 0 .5rem 0;
                button{
                    width: 3.1rem;
                    height: 1.3rem;
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
                    background: #ff3520;
                }
            }
        }
    }
</style>
