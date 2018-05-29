<template>
    <div class="network-box">
        <div class="net-text" @click="reload">系统升级中，点击返回</div>
    </div>
</template>

<script>
import units from '@/tools/units'
export default {    
    methods: {
        reload () {
            window.history.go(-1);
        }
    },
    created () {
        units.title.set('系统升级');
        this.$store.state.header.leftShow = false;
    }
}
</script>

<style scoped lang='scss'>
    .network-box{
        padding-top: 1.25rem;  
        position: fixed;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        z-index: 999;
        // background: url(../assets/img/network.png) center no-repeat;
        background:-moz-linear-gradient(top, #fff, #96b6e8);  
        background:-webkit-linear-gradient(top, #fff, #96b6e8);  
        background:linear-gradient(top, #fff, #96b6e8);  
        background-size: 100% 100%;
        .net-text{
            text-align: center;
            width: 100%;
            font-size: .5rem;
            position: absolute;
            bottom: 30%;
            left: 50%;
            transform: translateX(-50%);
            color: #fff;
        }
    }
</style>
