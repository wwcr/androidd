<template>
    <div class="network-box">
        <div class="net-text" @click="reload">服务器开小差，点击重新加载</div>
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
        units.title.set('网络错误');
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
        background: url(../assets/img/network.png) center no-repeat;
        background-size: 100% 100%;
        .net-text{
            text-align: center;
            width: 100%;
            font-size: .5rem;
            position: absolute;
            bottom: 30%;
            left: 50%;
            transform: translateX(-50%);
            color: #576998;
        }
    }
</style>
