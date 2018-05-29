<template>
    <div style="border:1px solid transparent;">
        <div class="vehicle-tool">
            <span @click="hrefDetailFn('peccancquery')">
                <img src="../../../src/assets/img/wc.png" alt="">
                <b>违章查询</b>
            </span>
            <span @click="hrefDetailFn('carcalculator')">
                <img src="../../../src/assets/img/cp.png" alt="">
                <b>车贷计算器</b>
            </span>
            <span @click="hrefDetailFn('vehicleevaluation')">
                <img src="../../../src/assets/img/cj.png" alt="">
                <b>车辆评估</b>
            </span>
        </div>
    </div>
</template>

<script>
import units from '@/tools/units'
export default {
    name: 'Vehicletool',
    methods: {
        hrefDetailFn (path) { //违章查询
            this.$router.push(path)
        }
    },
    created () {
        this.$store.state.header.right = false
        units.title.set('车融助手');
        this.$store.state.header.left = function () {
            location.href = '#/';
        };
    }
}
</script>
<style lang='scss' scoped>
    .vehicle-tool{
        background: #fff;
        margin-top: $top + 0.4rem;
        width: 100%;
        height: 3.8rem;
        display: flex;
        align-items: center;
        flex-wrap: wrap;
        span{
            width: 33.33333%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            img{
                height: .84rem;
            }
        }
        b{
            font-weight: normal;
            font-size: .38rem;
            color: #1e1e1e;
            margin-top:.3rem; 
        }
    }
</style>
